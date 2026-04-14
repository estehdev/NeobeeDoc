# environment variables
## APP MODE
### api-process-deployment
        - name: APP_MODEL_ENABLED
          value: "1"
        - name: TEMP_MAP_SELECT_KEY_TO_EXT_CODE
          value: "1"
        - name: CUSTOM_TABLE_IMPORT_ENABLED
          value: "1"
        - name: CUSTOM_TABLE_MIGRATION_ENABLED
          value: "1"
### frontend-deployment
add to all frontend apps
        - name: VUE_APP_APP_MODEL_ENABLED
          value: "1"
        - name: VUE_APP_TEMP_MAP_SELECT_KEY_TO_EXT_CODE
          value: "1"
## Database connection
## office file conversion
## onlyoffice
## Backend cache
## Frontend cache
## Signing app
       - name: APP_PATH
          value: "/download/NeobeeSignSetup_1_2_66.msi"
        - name: APP_VERSION
          value: "2.1.2.66"
        - name: APP_LEVEL
          value: "required"
        - name: APP_DOWNLOAD_ENABLED
          value: "1"
## graphql
process
        - name: APPSYNC_PROCESS_RECORD_API_URL
          value: "http://neobee-api-graphql/graphql/graphql"
frontend
       - name: VUE_APP_IS_GRAPHQL_ENABLED
          value: "1"
## services
       - name: API_USER
          value: "http://neobee-api-user/user"
        - name: API_INFRA
          value: "http://neobee-api-infra/infra"
        - name: API_MAIL
          value: "http://neobee-api-mail/mail"
        - name: API_PROCESS
          value: "http://neobee-api-process/process"
        - name: API_ATTACHMENT
          value: "http://neobee-api-attachment/attachment"
        - name: API_BIRT
          value: "http://neobee-api-birt/birt"
        - name: API_REST
          value: "http://neobee-api-rest/rest"
        - name: API_PROCESS
          value: "http://neobee-api-process/process"
        - name: API_EXTENDER
          value: "http://neobee-api-extender/extender"
        - name: API_ENDPOINT
          value: "http://neobee-api-base/neobee/api/base/endpoint"
        - name: API_CAT
          value: "http://neobee-api-cat/cat"
        - name: API_KNOWLEDGE
          value: "http://neobee-api-base/neobee/api/base/knowledge"
        - name: API_CALENDAR
          value: "http://neobee-api-base/neobee/api/base/calendar"
        - name: API_LLM
          value: "http://neobee-api-llm/llm"
