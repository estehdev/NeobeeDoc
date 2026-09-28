# Create ticket via REST (API key)

## Overview
External systems can create a ticket (process instance) in a Neobee project by calling the public REST service (MoRest2) with an API key. The API key is issued per tenant (company) in the administration and stored in the `es_process_api` table.

- **Type**: API endpoint
- **Owner**: Backend (MoRest2, MoProcess), Frontend (NeobeeAdminTenantFrontend)
- **Status**: Released
- **Last Updated**: 28.09.2026

---

## Description

Ticket creation from outside the platform is a two step procedure:

1. An administrator creates an **API key** for the tenant in the administration UI. The key is written to the `es_process_api` table together with the tenant's `company_id`.
2. The external system calls the **start process** endpoint of MoRest2, sending the key in the `X-KEY` header. MoRest2 resolves the tenant from the key, checks that the target project belongs to the same tenant and forwards the request to MoProcess, which creates and starts the ticket.

### Source code reference

| Part | Repository | Location |
| -- | -- | -- |
| REST endpoint | `MoRest2` | `code/core/src/main/java/net/esteh/rest/core/UtilResource.java` (`startProcess`) |
| API key lookup | `MoRest2` | `code/core/src/main/java/net/esteh/rest/core/manager/UtilManager.java` (`getCompanyIdByApiKey`) |
| Ticket creation | `MoProcess` | `code/core/src/main/java/net/esteh/moprocess/manager/ProcessRestPublicManager.java` (`startProcess`, action `start_process`) |
| API key administration (backend) | `MoProcess` | `code/core/src/main/java/net/esteh/moprocess/manager/ProcessApiManager.java`, REST path `/process_api` |
| API key administration (frontend) | `NeobeeAdminTenantFrontend` | `src/components/ProcessApi.vue`, route `/process-settings/api/apis` |

---

## API key administration

### Where in the UI

The key is managed in the **tenant administration** application (`NeobeeAdminTenantFrontend`):

**Process settings** (global settings, menu item `PROCESS_SETTINGS`) → **API** (`PROCESS_SETTINGS_API`) → tab **API** (route `/process-settings/api/apis`).

The page requires the permission `process_settings_page_client_main`.

The page lists all API keys of the tenant (columns *Name*, *Key*, actions). Inactive keys are shown greyed out; the *Active only* switch in the header filters them out.

### Creating a key

1. Click the **create** button in the page header.
2. Fill in **Name** (required, any descriptive text, e.g. the name of the external system).
3. **Key** is pre-filled with a freshly generated UUID. It can be replaced by any string (the field accepts up to 65535 characters). Copy this value, it is what the external system sends in the `X-KEY` header.
4. Save.

The frontend sends the following request to the MoProcess service (`API_PROCESS`, path `/process_api`):

```json
{
  "action": "create_process_api",
  "name": "External CRM",
  "key": "9d2f7c26-5b0d-4e0a-9d7a-1c7e6e6d0c11"
}
```

The backend (`ProcessApiManager.createProcessApi`) inserts a row into `es_process_api`:

| Column | Value |
| -- | -- |
| `name` | value of `name` |
| `key` | value of `key` |
| `company_id` | company of the logged in administrator |
| `status_id` | `1` (active) |

Response:

```json
{ "data": { "process_api_id": 12 }, "message": "", "messageCode": 1, "messageLevel": 1, ... }
```

### Editing or deactivating a key

Click the cog button in the row. The same modal opens with an additional **Active** switch. Saving sends:

```json
{
  "action": "update_process_api",
  "process_api_id": "12",
  "name": "External CRM",
  "key": "9d2f7c26-5b0d-4e0a-9d7a-1c7e6e6d0c11",
  "status_id": 0
}
```

Only the fields that are present and non-blank are updated. Setting `status_id` to anything other than `1` deactivates the key: the REST service only accepts keys with `status_id = 1`.

### Listing (for reference)

The list and details in the UI are read through `jsonquery` on the process service with `extCode` `PROCESS_API_LIST` (params `statusId`, `search`) and `PROCESS_API_DETAILS` (param `processApiId`). Both queries are restricted to the caller's `company_id`.

---

## Endpoint: start process

### Request

```
POST {REST_BASE_URL}/rest/util/start_process/process_project_id/{process_project_id}
```

`{REST_BASE_URL}` is the public host of the MoRest2 service for the environment (the service is deployed with the Quarkus root path `/rest`; inside the cluster it is reachable as `http://neobee-api-rest/rest`, see `API_REST` in the deployment environment).

`{process_project_id}` is the id of the project (`es_process_project.id`) in which the ticket is created. The project must be active (`status_id = 1`) and must belong to the same company as the API key.

#### Headers

| Header | Required | Description |
| -- | -- | -- |
| `X-KEY` | yes | API key from `es_process_api` (see above). |
| `Content-Type` | yes | `application/json` |

`X-CONTEXT` is the header used by internal calls (post functions). If `X-CONTEXT` is present it takes precedence and `X-KEY` is ignored. External callers send only `X-KEY`.

#### Body

The payload is wrapped in a `request_body` object. All ids are sent as **strings**.

```json
{
  "request_body": {
    "name": "Printer on 3rd floor not working",
    "task_type_id": "15",
    "ruser_id": "1024",
    "data_map": {
      "form.description.value": "Paper jam, error code E52",
      "form.priority.value": "2"
    }
  }
}
```

| Field | Required | Description |
| -- | -- | -- |
| `name` | yes | Ticket title (`es_process_instance.name`). |
| `task_type_id` | yes | Id of the task type (`es_task_type.id`) used for the ticket. Must be configured in the target project. |
| `ruser_id` | no | Id of the user (`es_ruser.id`) recorded as the ticket creator (`created_by_ruser_id`); it is also used as the user context for the start transition. When omitted the ticket is created by the system without a user. |
| `data_map` | no | Initial form field values. Keys have the form `form.<field_code>.value`, where `<field_code>` is the code of the form field (component) in the project. Only keys with scope `form` and property `value` are processed; other keys are ignored. Values are strings, or JSON structures for complex components (see below). |

Field values in `data_map` follow the same format as the `form.<field>.value` properties of a ticket: a plain string for simple components (text, number, date, single select by code) and a JSON array/object for complex components (multi select, catalog rows, files). The exact value format for a component can be checked in the *developer data* of an existing ticket in the UI.

### Processing

1. MoRest2 (`UtilResource.startProcess`) reads `X-KEY`, resolves `company_id` from `es_process_api` (only `status_id = 1`) and resolves `company_id` of the project from `es_process_project` (only `status_id = 1`). Both must match.
2. MoRest2 forwards the call to MoProcess (`{API_PROCESS}/process_rest_public`) as action `start_process` with `process_project_id`, `task_type_id`, `name`, `ruser_id` and `data_map`.
3. MoProcess (`ProcessRestPublicManager.startProcess`), in one transaction:
   - creates a process draft (`executeCreateProcessDraft`) with a new EUID,
   - writes the `data_map` values to the form fields (`saveProcessInstanceProperties`),
   - starts the draft (`executeStartProcessDraft`) with the given `name`: generates the ticket code (`ext_code`, from the project template or the project code + counter), sets the default assignee and creator, sends the `START` signal to the initial state (which runs the configured post functions) and creates the process document if the project is document based.
4. The resulting `es_process_instance` row is returned.

### Response

Success (`HTTP 200`): standard envelope with the created process instance in `data`. `data` contains the columns of `es_process_instance` plus `process_euid`; the most useful are:

```json
{
  "data": {
    "id": 48213,
    "ext_code": "HD-1042",
    "process_euid": "0f4a2d3e-8b6c-4c8f-9c3a-6e1b2f7d9a10",
    "name": "Printer on 3rd floor not working",
    "process_project_id": 7,
    "task_type_id": 15,
    "company_id": 3,
    "status_id": 1,
    "...": "..."
  },
  "version": "beta",
  "message": "",
  "messageCode": 1,
  "messageLevel": 1,
  "uuid": "…",
  "hash": "…"
}
```

`id` is the ticket id, `ext_code` is the ticket code shown in the UI.

Errors:

| HTTP status | When | Body |
| -- | -- | -- |
| `401 Unauthorized` | Neither `X-KEY` nor `X-CONTEXT` header is present. | `{"data":{}, "message":"Unauthorized", "messageCode":2, "messageLevel":4, ...}` |
| `403 Forbidden` | Key not found or inactive, project not found or inactive, or key and project belong to different companies. | `{"data":{}, "message":"Forbidden operation", ...}` |
| `500 Internal Server Error` | Invalid body (missing `name` / `task_type_id`, not a JSON object, malformed `data_map` key), unknown `task_type_id`, or any error while creating the ticket. | `{"data":{}, "message":"Server error", ...}` |

The error body is the same envelope with an empty `data` object and `messageCode` / `messageLevel` set to the error values. Details of a `500` are only available in the MoRest2 and MoProcess logs.

### curl example

```bash
curl -X POST "https://<rest-host>/rest/util/start_process/process_project_id/7" \
  -H "Content-Type: application/json" \
  -H "X-KEY: 9d2f7c26-5b0d-4e0a-9d7a-1c7e6e6d0c11" \
  -d '{
    "request_body": {
      "name": "Printer on 3rd floor not working",
      "task_type_id": "15",
      "ruser_id": "1024",
      "data_map": {
        "form.description.value": "Paper jam, error code E52",
        "form.priority.value": "2"
      }
    }
  }'
```

Minimal call (no reporter, no form values):

```bash
curl -X POST "https://<rest-host>/rest/util/start_process/process_project_id/7" \
  -H "Content-Type: application/json" \
  -H "X-KEY: 9d2f7c26-5b0d-4e0a-9d7a-1c7e6e6d0c11" \
  -d '{"request_body": {"name": "Ticket from external system", "task_type_id": "15"}}'
```

---

## Other endpoints that accept `X-KEY`

Only the endpoints below accept an API key. All other MoRest2 endpoints (including `/util/create_process/...` and `/util/initiate_process/...`) require the internal `X-CONTEXT` header and are not callable from outside.

| Method | Path | Description |
| -- | -- | -- |
| `POST` | `/rest/util/start_process/process_project_id/{process_project_id}` | Create and start a ticket (this document). Key company must match the project company. |
| `GET` | `/rest/util/counter/company_id/{company_id}/name/{name}?prefix={prefix}` | Read a company counter by name. Key company must match `{company_id}`. |
| `POST` | `/rest/util/download` | Download a file from a URL given in `request_body.url`, returned base64 encoded in `data.data`. Key only has to exist and be active. |

---

## Notes and limitations

- One key is valid for the whole tenant: it can create tickets in **any active project** of that company. There is no per project or per task type restriction.
- The key is stored and compared in plain text. Treat it like a password and rotate it by creating a new key and deactivating the old one.
- Requests without `X-KEY` and `X-CONTEXT` are rejected, but there is no rate limiting on the endpoint.
- The ticket is started as a system action (`isSystem = true`), so post functions of the initial transition run without a logged in user context. Use `ruser_id` when the process logic needs a reporter.
