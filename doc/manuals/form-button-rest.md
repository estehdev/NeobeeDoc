# Form button (REST)

## Overview
The Form Button (REST) is a UI component used to initiate custom HTTP requests from a form.

- **Type**: UI Component
- **Owner**: Frontend
- **Status**: Released
- **First Released**: 05.09.2024
- **Last Updated**: 03.09.2025

---

## Description

The **Form Button (REST)** component supports two operation modes: **Simple** and **Advanced**.

### Simple Mode Configuration

In Simple mode, users manually configure the HTTP request by specifying the following settings:

#### Request URL

The endpoint URL where the HTTP request will be sent. This should be a fully qualified URL (e.g., `https://api.example.com/data`). Ensure the URL is correct, as the request will fail if the endpoint is unreachable or malformed.

#### HTTP Method

Defines the HTTP method used for the request. Supported methods are:

- **GET** — Retrieves data from the specified endpoint.
- **POST** — Sends data to the endpoint to create or update resources.

**Note:** POST requests are only supported when performing the request in the background (see button click behaviors below).

#### Request Header

Specifies the `Content-Type` header to include in the outgoing HTTP request. This tells the server the format of the data being sent. Common values include:

- `application/json`
- `application/x-www-form-urlencoded`
- `text/plain`

Setting the correct `Content-Type` ensures the server correctly interprets the request payload.

#### Response Header

Defines the expected `Content-Type` of the HTTP response. This helps the component correctly parse the response data. Typical values include:

- `application/json`
- `text/html`
- `text/plain`

Configuring this header correctly ensures the response can be processed or displayed as intended.

#### Button Click Behaviors

Users can specify what happens when the button is clicked. The supported options are:

- **Perform the request in the background**  
   The request is sent silently without interrupting the user interface. This is the only behavior that supports POST requests. The response can be handled programmatically or ignored.

- **Open request in a popup window**  
   The request is sent by opening a new popup window, displaying the response. This behavior supports GET requests only.

- **Open request in a new browser tab**  
   Similar to the popup option, but the response opens in a new browser tab. This also supports GET requests only.


### Advanced Mode

In **Advanced Mode**, users define a **process function** that calls a REST endpoint. When the button is clicked, the request is sent to the `ProcessAPI`, which executes the process function and returns the result.

#### How It Works

1. **User selects a predefined REST endpoint**  
   The system provides a list of predefined REST endpoint configurations. Each configuration defines:  
   - The target URL  
   - HTTP method  
   - Required and optional parameters  
   - Headers  
   - Response mapping logic

2. **User fills out required parameters**  
   The UI prompts the user to input any parameters defined by the selected endpoint configuration. This creates the **process function**.

3. **Frontend (Form Button) triggers the `ProcessAPI`**  
   When the button is clicked, the frontend calls the internal `ProcessAPI`, passing:  
   - The process function id, which points to the selected REST endpoint configuration
   - The user-provided parameters

4. **ProcessAPI handles the request execution**  
   The `ProcessAPI` performs the following:  
   - Resolves the full REST endpoint configuration  
   - Substitutes all parameters into the request  
   - Executes the HTTP request to the external system  
   - Applies any response mapping rules  
   - Returns the final result to the frontend

#### Key Benefits

- **Centralized Configuration** — All REST endpoint logic is managed in one place, reducing duplication and ensuring consistency.
- **Secure Execution** — Credentials, headers, and sensitive logic stay on the server side.
- **Flexible Response Mapping** — Allows transforming complex responses into usable values for the UI or workflows.
- **Reusable Endpoints** — REST configurations can be reused across multiple buttons or workflows.

#### When to Use Advanced Mode

Use **Advanced Mode** when:

- The request logic is too complex for Simple Mode  
- The same REST endpoint is used across multiple forms or processes  
- You need dynamic response mapping or post-processing  
- Security or compliance requires server-side execution

