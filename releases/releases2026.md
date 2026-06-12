# NeoBee Releases 2026
## June, week II
### Fixes
- Ticket Priority Display – Fixed priority display issues in ticket lists (NeobeeFrontendSettings v3.66.1, NeobeeFrontendProject v3.66.1, NeobeeFrontendCentral v3.66.1, NeobeeFrontendDeveloper v3.66.2).
- Document Content Page – Restored the document content page (/document/content/...) on the new portal after it was missed during migration (NeobeeFrontendCentral v3.66.2).
- Application Build Export – Fixed an issue where application builds exported form item definitions field by field instead of exporting the complete es_form_item definition (MoProcess v3.65.36).
- Signature API Integration – Updated all requests to the MoSignature service to use BaseAPI endpoints (MoCentralFrontend v1.0.431, NeobeeFrontendSettings v3.65.29, NeobeeFrontendProject v3.65.21, NeobeeFrontendCentral v3.65.36, NeobeeFrontendDeveloper v3.65.22).
### Improvements
- NeoChatPage – Added support for displaying chunk messages received through notifications and improved the chat experience by introducing a new chat action, upload close action, ticket ext_code display, enhanced dropdown rendering, tool approval menu actions, and message scrolling behavior.
### New Features
- Private WebSocket Channel – Implemented authenticated private WebSocket channels with user-level message filtering based on company and user identifiers, enabling support for private notifications and messaging (NeobeeGraphql v3.65.6, MoProcess v3.65.38, MoLlm v3.65.10, MoCentralFrontend v1.0.432, NeobeeFrontendSettings v3.65.30, NeobeeFrontendProject v3.65.23, NeobeeFrontendCentral v3.65.39, NeobeeFrontendDeveloper v3.65.23).
- Keycloak User Refresh – Added a mechanism for detecting newly created users in Keycloak and refreshing user availability within the application (MoCentralFrontend v1.0.430, NeobeeFrontendSettings v3.65.25, NeobeeFrontendProject v3.65.18, NeobeeFrontendCentral v3.65.33, NeobeeFrontendDeveloper v3.65.19).
- Markup Component Support – Added support for rendering markup content through a dedicated component on Vue 3 portals (NeobeeFrontendSettings v3.65.28, NeobeeFrontendProject v3.65.20, NeobeeFrontendCentral v3.65.35, NeobeeFrontendDeveloper v3.65.21).
- AI Chat HTML Rendering – Implemented rendering of HTML content generated from Markdown documents within AI Chat (NeobeeFrontendSettings v3.65.34, NeobeeFrontendProject v3.65.29, NeobeeFrontendCentral v3.65.44, NeobeeFrontendDeveloper v3.65.26).
## June, week I
### Fixes
- AdvancedTable – Fixed value refresh issues when AdvancedTable components are used inside subforms (MoCentralFrontend v1.0.417, NeobeeFrontendSettings v3.65.16, NeobeeFrontendProject v3.65.11, NeobeeFrontendCentral v3.65.16, NeobeeFrontendDeveloper v3.65.13).
- AdvancedTable Files – Fixed file loading in multiform popups by ensuring processInstanceId is properly passed (MoCentralFrontend v1.0.417, NeobeeFrontendSettings v3.65.16, NeobeeFrontendProject v3.65.11, NeobeeFrontendCentral v3.65.16, NeobeeFrontendDeveloper v3.65.13).
- Form Tables – Added minimum row height to improve table rendering consistency on forms (MoCentralFrontend v1.0.419, NeobeeFrontendSettings v3.65.18, NeobeeFrontendProject v3.65.14, NeobeeFrontendCentral v3.65.18, NeobeeFrontendDeveloper v3.65.15).
- State Error Indicators – Fixed incorrect display of error-state warnings while editing post functions (MoCentralFrontend v1.0.419, NeobeeFrontendSettings v3.65.18, NeobeeFrontendProject v3.65.14, NeobeeFrontendCentral v3.65.18, NeobeeFrontendDeveloper v3.65.15).
- AdvancedTable Actions – Fixed inability to delete an action currently being edited (MoCentralFrontend v1.0.419, NeobeeFrontendSettings v3.65.18, NeobeeFrontendProject v3.65.14, NeobeeFrontendCentral v3.65.18, NeobeeFrontendDeveloper v3.65.15).
- Form Schema Administration – Corrected label inconsistencies in form schema administration pages (MoCentralFrontend v1.0.419 and related frontend applications).
- Form Validation – Fixed validation behavior for text, email and numeric fields, including missing email validation and hidden validation messages (NeobeeFrontendSettings v3.65.20, NeobeeFrontendProject v3.65.15, NeobeeFrontendCentral v3.65.19, NeobeeFrontendDeveloper v3.65.16).
- Process Module Details – Fixed SQL syntax issue in the process module details query (MoProcess v3.65.28).
- Application Build Popup – Fixed title formatting issues in the application build popup (NeobeeFrontendSettings v3.65.23).
- Empty Tables – Fixed duplicate border rendering in empty table views (NeobeeFrontendSettings v3.65.22, NeobeeFrontendProject v3.65.16, NeobeeFrontendCentral v3.65.20, NeobeeFrontendDeveloper v3.65.17).
### Improvements
- App Store – Added pagination to the application listing page.
- Error Monitoring – Simplified error loading by using a single query independent of the APP_MODEL_ENABLEDconfiguration (NeobeeFrontendSettings v3.65.19).
- Error Monitoring – Error detail navigation now uses direct links that can be opened in a separate browser tab (NeobeeFrontendSettings v3.65.21).
- Application Export – Added validation for App Map references during application build to prevent exporting invalid permission scheme or SMTP endpoint references (MoProcess v3.65.11).
- Issue List Performance – Added MySQL execution time limit for get_issue_list queries to improve system stability (MoProcess v3.65.31).
### New Features
- Custom Table Dropdowns – Added support for using Custom Tables as a data source for dropdown components (MoCentralFrontend v1.0.418, NeobeeFrontendSettings v3.65.17, NeobeeFrontendProject v3.65.13, NeobeeFrontendCentral v3.65.17, NeobeeFrontendDeveloper v3.65.14).
- Application Export – Added support for exporting App Dashboard menus and groups, including related administration and application assignment management (NeobeeBase v3.65.9, NeobeeFrontendSettings v3.65.21, MoProcess v3.65.27).
- Application Build Audit Trail – Added developer tracking information (developer_username and developer_user_fullname) to application builds (MoProcess v3.65.31).
- AI Spaces – Added process_project_id, issue_type_id, and form_id fields to AI Space configuration forms.

## May, week IV
### Fixes
- Application Export Logs – Fixed incorrect entity reporting in export/build logs related to NRN conversion processing (MoProcess v3.64.31).
- Keycloak Configuration – Fixed issues with applying newly introduced Keycloak environment configuration values (MoCentralFrontend v1.0.409, NeobeeFrontendSettings v3.65.3, NeobeeFrontendProject v3.65.3, NeobeeFrontendCentral v3.65.4, NeobeeFrontendDeveloper v3.65.5).
- Description Component Value Persistence – Fixed unexpected value saving caused by the Description component emitting change events when no actual changes occurred (MoCentralFrontend v1.0.410, NeobeeFrontendSettings v3.65.5, NeobeeFrontendProject v3.65.4, NeobeeFrontendCentral v3.65.7, NeobeeFrontendDeveloper v3.65.6).
- Invalid Form Value Handling – Implemented validation and automatic deactivation of empty form records, preventing submission of invalid values from the frontend (MoCat v3.65.1, MoCentralFrontend v1.0.411, NeobeeFrontendSettings v3.65.11, NeobeeFrontendProject v3.65.7, NeobeeFrontendCentral v3.65.11, NeobeeFrontendDeveloper v3.65.9).
### Improvements
- Form Item Usage Detection – Implemented dependency detection for form items, providing visibility into where an item is referenced before deletion (visibility rules, editability, required fields, actions, etc.) (MoCentralFrontend v1.0.407, NeobeeFrontendSettings v1.0.298, NeobeeFrontendProject v1.0.207, NeobeeFrontendCentral v1.0.213).
- Frontend Performance Optimization – Introduced the first phase of frontend performance improvements, including CSS, font, static resource, look&feel  loading optimizations (MoCentralFrontend v1.0.410, NeobeeFrontendSettings v3.65.5, NeobeeFrontendProject v3.65.4, NeobeeFrontendCentral v3.65.7, NeobeeFrontendDeveloper v3.65.6).
- Application Export – Added NRN conversion for local_copy_table_id and sync_config.source_table_id references in es_process_custom_table.definition (MoProcess v3.65.5).
- Application Build Validation – Added validation of AppMap resource references during application build to prevent packaging projects with missing permission scheme or SMTP endpoint mappings (MoProcess v3.65.11).
### New Features
- Keycloak Configuration Environment Variables – Added new environment variables for Keycloak URL, realm, and client ID configuration (MoCentralFrontend v1.0.407, NeobeeFrontendSettings v1.0.298, NeobeeFrontendProject v1.0.207, NeobeeFrontendCentral v1.0.213).
- App Dashboard – Added new APP_DASHBOARD_SLA_BREACH query for AppDashboard reporting (NeobeeBase v3.64.8).
- AI Config Designer – Added support for Custom Table nodes and configurable filtering options for Content Index and Custom Table components based on user and company context attributes.
- NeoChat – Added support for displaying TOOL_CALL and TOOL_RESULT messages in chat conversations.Custom Table Administration – Added mcp_enabled and mcp_description fields to custom table configuration forms.
## May, week III
### Fixes
- Permission Scheme Export – Excluded SINGLE_USER types and non-application groups from permission scheme export (MoProcess v3.64.10).
- Ticket Creation – Fixed issue where pressing Enter in the “Name” field could block the Create button during ticket creation (MoCentralFrontend v1.0.399, NeobeeFrontendCentral v1.0.200, NeobeeFrontendSettings v1.0.284, NeobeeFrontendProject v1.0.196).
- Approval Controls – Expanded split approval buttons and adjusted layout to properly display the “Outside of responsibility” label (MoCentralFrontend v1.0.400).
- Ticket Creation Value Mapping Priority – Fixed issue where default form values were overriding transition parameters when opening ticket creation forms via transition popup (MoCentralFrontend v1.0.406, NeobeeFrontendSettings v1.0.291, NeobeeFrontendProject v1.0.202, NeobeeFrontendCentral v1.0.205).
- Notification Colors – Fixed notification color inconsistency on Vue 3 applications (Central, Settings, Project) affecting bottom-right notification display (MoCentralFrontend v1.0.406, NeobeeFrontendSettings v1.0.291, NeobeeFrontendProject v1.0.202, NeobeeFrontendCentral v1.0.205).
- AppDashboardDatepickerReport – Fixed range datepicker popup positioning issue where the popup could appear behind page content (MoCentralFrontend v1.0.402).
### Improvements
- Issue Field – Simplified ticket list display on forms in both multi and single selection modes (MoCentralFrontend v1.0.400, v1.0.401, NeobeeFrontendSettings v1.0.285/v1.0.286, NeobeeFrontendProject v1.0.197/v1.0.199, NeobeeFrontendCentral v1.0.201/v1.0.202).
- Permission Schemes – Restricted available resources in permission schemes while working in application mode (MoCat v3.64.3, MoUser v3.64.2, MoCentralFrontend v1.0.400, NeobeeFrontendSettings v1.0.285, NeobeeFrontendProject v1.0.197, NeobeeFrontendCentral v1.0.201).
- Utility Applications – Refactored API queries and jsonquery logic to use dynamically resolved utility applications instead of hardcoded neobee:neobeeutil references (MoProcess v3.64.17, MoCat v3.64.5, MoUser v3.64.3).
- Form Administration – Improved role display in form item configuration by showing role name, code, and associated application during lookup rendering (MoCentralFrontend v1.0.404, NeobeeFrontendSettings v1.0.288, NeobeeFrontendProject v1.0.201, NeobeeFrontendCentral v1.0.204).
- Application Build – Added validation of resource ownership against referenced applications during application build process and improved build logs (MoProcess v3.64.27).
- Application Build List – Implemented paging support for application build history pages (MoProcess v3.64.28, NeobeeFrontendSettings v1.0.292).
- App Instance Readonly – Extended readonly support across all pages and functionalities in NeobeeFrontendProject, including backend 403 validation handling.
### New Features
- Post Functions – Implemented support for direct text input of resource references (form/table/json/code) when Remote Server mode is enabled (MoCentralFrontend v1.0.403, NeobeeFrontendSettings v1.0.287, NeobeeFrontendProject v1.0.200, NeobeeFrontendCentral v1.0.203).
- AI Config Designer – Implemented AI configuration designer with VueFlow-based node management, Agent/LLM configuration support, MCP/RAG handling, auto-save with debounce, auto layout, project integration, and advanced node interaction features.
- AI Config Designer – Added project section with mcp_enabled support and automatic layout synchronization based on configuration definitions.
## May, week II
### Fixes
- Ticket Creation via Task – Fixed issue with homepage opening from AppDashboard during ticket creation workflow.
- Approval Section – Fixed missing mapping list display on homepage approval configuration.
### Improvements
- Ticket List Actions – Added support for displaying action buttons in ticket lists, disabled by default.
- JWT / User Details – Moved JWT-related user fields (ruser_id, ruser_euid, company_id, company_euid) to get_user_details, removing dependency on token claims (MoUser v3.64.1, MoCentralFrontend v1.0.392, NeobeeFrontendSettings v1.0.277, NeobeeFrontendProject v1.0.191, NeobeeFrontendCentral v1.0.195).
Process Functions – Removed app_instance_id restriction from custom table listing queries in process functions (MoCentralFrontend v1.0.393, NeobeeFrontendSettings v1.0.279, NeobeeFrontendProject v1.0.192, NeobeeFrontendCentral v1.0.196).
- Applications – Blocked reinstall of source system applications and prevented installation of older or equal application versions.
- App Instance Readonly – Extended readonly handling across project application components, including UI restrictions and backend 403 Forbidden validation.
- Ticket Lists – Added readonly handling and approval section fixes for locked app instances.
### New Features
- Application Translations – Implemented new application translation key format using NRN and app_instance_id, with support added for states, transitions, form components, resolutions, priorities, process modules, and related resources (MoProcess v3.64.6, MoCat v3.64.1, MoCentralFrontend v1.0.391, NeobeeFrontendCentral v1.0.193, NeobeeFrontendProject v1.0.189, NeobeeFrontendSettings v1.0.273).
- Application Translations – Improved export format for application translations (MoCat v3.64.2, NeobeeBase v3.64.1, MoCentral v3.64.2, MoCentralFrontend v1.0.392, NeobeeFrontendSettings v1.0.277, NeobeeFrontendProject v1.0.191, NeobeeFrontendCentral v1.0.195).
- Application Translations – Implemented Excel import support for application translations (MoCentral v3.64.3, NeobeeFrontendSettings v1.0.281).
- Approval Tab – Enabled removal of selected values from the “Exclude – Isključi” field and added unsaved changes warning popup.
## May, week I
### Fixes
- Approval Controls – fixed issue causing voting controls not to appear after split approval changes (MoCentralFrontend v1.0.384, NeobeeFrontendCentral v1.0.187).
- Application Installation – added duplicate validation by ext_code during manual application installation and UI-based creation to prevent duplicate applications (MoProcess v3.63.21, NeobeeFrontendSettings v1.0.267).
### Improvements
- Signed Approval State – improved approval status display by adding dedicated messages for signed items and approvals currently in progress (MoCentralFrontend v1.0.386, NeobeeFrontendCentral v1.0.190).
- Application Build – installation file inside exported ZIP packages is now standardized as app.json while ZIP archive naming remains unchanged (MoProcess v3.63.21).
### New Features
- Custom Tables – implemented support for new is_locked flag in custom table administration (MoProcess v3.63.19, MoCentralFrontend v1.0.385, NeobeeFrontendSettings v1.0.264).
- Application Installation – introduced new skip_tables_on_import flag available during manual application import (NeobeeFrontendSettings v1.0.386, MoProcess v3.63.22).
- Application Translation Export – implemented export of language items as part of the application build process (MoProcess v3.63.25).
- Remove-only Mode – added form dropdown configuration allowing only value removal without adding new entries.
## April, week IV
### Fixes
- AppMap Mapping Display – fixed formatting issue for selected values in locked mapping fields (MoCentralFrontend v1.0.380, NeobeeFrontendSettings v1.0.256, NeobeeFrontendProject v1.0.180, NeobeeFrontendCentral v1.0.180).
### Improvements
- Split Approval – redesigned UI for split/individual approval, including support for marking items as “Opinion” (MoCentralFrontend v1.0.378, MoCentralFrontend v1.0.379).
- AppDashboard Filters – implemented filter combination logic for issue list (MoCentralFrontend v1.0.379).
- AppMap Export – updated export behavior to exclude map_reference_to when is_export_enabled is not set; flag renamed and hidden for non-exportable entities (MoCentralFrontend v1.0.381, NeobeeFrontendSettings v1.0.257, NeobeeFrontendProject v1.0.181, NeobeeFrontendCentral v1.0.181, MoProcess v3.63.6).
- User Language Selection – extended available languages on user details page (Hungarian, Albanian, Macedonian, Turkish, Bulgarian) (MoCentralFrontend v1.0.382, NeobeeFrontendSettings v1.0.259, NeobeeFrontendProject v1.0.182, NeobeeFrontendCentral v1.0.182).
### New Features
- AppMap Types – added support for new appmap types content_index and ai_config; included in REST endpoint parameter definitions and process functions via appmap reference (MoCentralFrontend v1.0.381, NeobeeFrontendSettings v1.0.257, NeobeeFrontendProject v1.0.181, NeobeeFrontendCentral v1.0.181, MoProcess v3.63.6).
- Content Index – implemented administration page with options to deactivate or permanently delete entries, including confirmation flow; added application selection component and updated handling via status_id.
## April, week III
### Fixes
- Default Form Values – fixed issue with applying default values in forms (MoCentralFrontend v1.0.369).
- Select Component (TEMP_MAP_SELECT_KEY_TO_EXT_CODE) – fixed ID resolution issue by moving lookup logic to the server, where ID is resolved based on ext_code (MoCentralFrontend v1.0.371, MoCat v3.62.2).
- Text Fields Rendering – fixed issues with rendering diacritic characters (ŠČĆŽ) in Firefox (MoCentralFrontend v1.0.373, v1.0.375, NeobeeFrontendSettings v1.0.253, NeobeeFrontendProject v1.0.175, NeobeeFrontendCentral v1.0.175).
### Improvements
- AppDashboard ASCII Search – introduced ASCII search mode for dashboard tables and dropdowns (custom table sources), enabling SQL-based ASCII conversion for both search terms and columns (MoCentralFrontend v1.0.372, v1.0.374, NeobeeFrontendCentral v1.0.170, v1.0.173, MoProcess v3.62.12).
- User Group Administration – added paging to the user groups page (previously all groups were listed without limits), highlighted inactive groups, introduced sorting by group name (MoUser v3.62.5, MoCentralFrontend v1.0.376, NeobeeFrontendSettings v1.0.254, NeobeeFrontendProject v1.0.176, NeobeeFrontendCentral v1.0.176).
### New Features
- VTL Context in Default Values – implemented evaluation of VTL context for setting default form values (MoCentralFrontend v1.0.369, MoProcess v3.62.11).
## April, week II
### Fixes
- App Context Key – limited maximum length of the key field to 255 (MoCentralFrontend v1.0.365, NeobeeFrontendSettings v1.0.245).
### Improvements
- User Group Details – introduced a dedicated details tab for user groups (aligned with user details view); group code is now hidden outside the details tab (MoCentralFrontend v1.0.362, NeobeeFrontendSettings v1.0.242, NeobeeFrontendProject v1.0.167, NeobeeFrontendCentral v1.0.165).
- App Context – removed app_context from appmap types; export procedure updated to exclude the value field (MoCentralFrontend v1.0.367, NeobeeFrontendSettings v1.0.247).
### New Features
- App Context (Config) – implemented support for new map_type app_context, enabling mappings to the new es_app_context table for application-level configurations (MoProcess v3.62.6, MoCentralFrontend v1.0.364, NeobeeFrontendSettings v1.0.244).
## April, week I
### Fixes
- AppDashboard DatePicker – Fixed incorrect positioning logic (MoCentralFrontend v1.0.349, NeobeeFrontendCentral v1.0.156).
- AppDashboard Issue List – Fixed sorting not being applied from filters (MoCentralFrontend v1.0.350, NeobeeFrontendCentral v1.0.157).
- App Export – Fixed missing form reference mapping in subforms (MoProcess v3.61.5).
- App Export – Updated process function export to prevent failures when referenced file templates are missing (MoProcess v3.61.10).
- AppDashboard DatePicker Report – Fixed missing event payload emission when mapping is not defined (MoCentralFrontend v1.0.354).
- Form Administration – Fixed custom time validator issue in time components (NeobeeFrontendProject v1.0.163, NeobeeFrontendSettings v1.0.237).
- Ticket Details - Fixed incorrect display of alternative transition names (including translations) when actions are not available (MoCentralFrontend v1.0.361, NeobeeFrontendCentral v1.0.164).
- AppDashboard Table – Fixed conditional formatting issues for jsonquery and data variants.
### Improvements
- AppDashboard – Added option to disable responsive behavior, preserving grid layout across all screen resolutions (MoCentralFrontend v1.0.348, NeobeeFrontendCentral v1.0.155).
- Reports – Removed BIRT reports without associated files from Reports page (NeobeeBase v3.61.2).
- Ticket Locking – Updated behavior to keep forms locked in code-type states, with transitions available only to users with debugging enabled (MoCentralFrontend v1.0.356).
- Approval Workflow (Tag-based) – Improved tag display and handling of partially processed approvals (MoCentralFrontend v1.0.360, NeobeeFrontendCentral v1.0.163)
- NeoChat Sidebar – Improved responsiveness and layout on smaller screens.
### New Features
- Approval Workflow (Tag-based) – Implemented initial version of split approval mechanism based on tags, including deadline handling and partial approval support (MoCentralFrontend v1.0.355).
- AppDashboard – Added new queries in MoDashboard API to support chart creation in dashboards.
## March, week V
### Fixes
- Ticket Link – Added validation for status_id=1 when accessing tickets via code-based links (MoCentralFrontend v1.0.330, NeobeeFrontendCentral v1.0.139, MoProcess v3.60.15).
- Ticket Details – Fixed issue where ZIP download popup was rendered behind other content (MoCentralFrontend v1.0.315).
### Improvements
- AppDashboard DatePicker – Added automatic emission of default value (MoCentralFrontend v1.0.347, NeobeeFrontendCentral v1.0.154).
- NeoChat – Added chat_euid validation to ensure messages are displayed only in the correct chat context.
### New Features
- AppDashboardTable – Enabled JSON column formatting with “row” context support, allowing access to values from other columns during client-side evaluation (MoCentralFrontend v1.0.331, NeobeeFrontendCentral v1.0.140).
- Keycloak Integration – Enabled Keycloak authentication across Central, Settings, and Project applications on a1 environment (MoCentralFrontend v1.0.346, NeobeeFrontendSettings v1.0.235, NeobeeFrontendProject v1.0.161, NeobeeFrontendCentral v1.0.153).
## March, week IV
### Fixes
- Custom Tables orderBy – Fixed incorrect automatic addition of ASC parameter (MoProcess v3.60.10).
- Subtask View – Fixed popup sizing issue when opened from parent ticket (MoCentralFrontend v1.0.323).
- Ticket Details Page – Fixed layout issue preventing independent scrolling of sections (MoCentralFrontend v1.0.324, NeobeeFrontendCentral v1.0.133).
- Fixed issue with storing formatted numeric values (now stored as raw numbers and formatted on display).
### Improvements
- Ticket Filters – Added support for integer-type fields in ticket and form filters (MoCentralFrontend v1.0.315, NeobeeFrontendCentral v1.0.128, NeobeeFrontendSettings v1.0.206).
- Post Functions – Improved UI filtering to display only relevant sources, current app or neobeeutil app (MoCentralFrontend v1.0.317, NeobeeFrontendSettings v1.0.208, NeobeeFrontendProject v1.0.144, NeobeeFrontendCentral v1.0.130, MoProcess v3.60.11, MoCat v3.60.1).
- Project Creation – Automatically generates a default permission scheme if missing and establishes appmap linkage (MoProcess v3.60.14).
- Form Item Conditions – Legacy Conditions tab hidden when empty, preventing adding deprecated conditions to new components while keeping existing ones visible (MoCentralFrontend v1.0.327, NeobeeFrontendSettings v1.0.215, NeobeeFrontendProject v1.0.149).
- AI Configuration UI – Initial interface setup and data visualization prepared on admin tenant frontend.
### New Features
- OpenSearch AppDashboard – Implemented index selection across all OpenSearch components, along with backend support for reading index_id from request parameters; added fixed category filtering mode with single-category constraint (MoCentralFrontend v1.0.311, NeobeeBase v3.60.3).
- AppDashboard OpenSearch Results – Added configuration for opening result links directly via title click, with optional new tab behavior (MoCentralFrontend v1.0.328, NeobeeFrontendCentral v1.0.136).

## March, week III
### Fixes
- Nested subforms – Fixed issue with subform rendering inside another subform (MoCentralFrontend v1.0.296).
- Application tags (build process) – Fixed issue with tag application during build execution.
- Form item list – Removed redundant form_item_app_instance_id field from UI display.
- App Dashboard locked state – Disabled unsupported actions in locked mode and improved overall validation logic.
### Improvements
- Translation export (forms) – Enhanced export by adding the “default” column, excluding system components, and improving UI behavior and visibility rules for application-bound forms (MoProcess v3.60.1, MoCentralFrontend v1.0.298).
- Application tags (App Store) – Completed full implementation of tag-based filtering and build tagging logic across environments, including remote repository scenarios.
- OpenSearch AppDashboard – Introduced support for index selection per component by enabling backend index_id handling and partial frontend integration.
- State type management – Improved application selection during state type creation and editing (MoProcess v3.60.5, NeobeeFrontendSettings v1.0.199).
### New Features
- Translation export – Implemented translation export mechanism (MoCentral v3.59.3, NeobeeFrontendSettings v1.0.104, NeobeeFrontendProject v1.0.134, MoCentralFrontend v1.0.295). 
- AppDashboard – Added advanced configuration for dropdown components using custom tables, including sorting options (column and direction) and automatic value selection with event emission (MoProcess v3.60.1, MoCentralFrontend v1.0.300, NeobeeFrontendCentral v1.0.122).
- Label / Alert component – Introduced new “success” type for visual feedback (MoCentralFrontend v1.0.301, NeobeeFrontendSettings v1.0.197, NeobeeFrontendProject v1.0.138, NeobeeFrontendCentral v1.0.123).
- App Dashboard duplication – Implemented functionality for duplicating dashboards with all components, actions, and subscriptions, without linkage to the source dashboard.

## March, week II
### Fixes
- Improved hierarchical filtering and permission validation logic by aligning path comparison between orgunitidspath and unididpath and fixed duplicate ticket entries caused by incorrect query conditions(MoProcess v3.59.7, MoProcess v3.59.10).
- Remote endpoints administration – Fixed issue preventing parameter input and ensured proper reflection of stored secrets (NeobeeBase v3.59.7).
- Menu items administration – Restored visibility of the control for deactivating individual menu items (NeobeeFrontendSettings v1.0.184).
### Improvements
- User delegation (Tickets page) – Enabled persistence of selected substitute user when leaving the page, with automatic reset on project change or expired/invalid authorization (MoCentralFrontend v1.0.278).
- NeoChat – Added Markdown parser for rendering AI responses as HTML (NeobeeFrontendCentral v1.0.111).
File versions – Added display of the user who created each file version (MoCentralFrontend v1.0.281).
- Look & Feel – Moved default user form selection into the Look & Feel configuration section (MoCompany v3.59.2, MoCat v3.59.2, MoCentralFrontend v1.0.284, NeobeeFrontendSettings v1.0.186, NeobeeFrontendProject v1.0.130).
- Application tags (App Store) – Implemented tag-based filtering for applications and builds, including logic for assigning tags to builds with automatic removal from other builds.
### New Features
- Banners / notifications system – Implemented full functionality including backend (data model, CRUD operations, and user-specific filtering) and frontend (administration and display).
- Look & Feel configuration – Added option to control visibility of the Help section in the top menu (MoCompany v3.59.3, MoCentralFrontend v1.0.285, NeobeeFrontendSettings v1.0.187, NeobeeFrontendCentral v1.0.116).
## March, week I
### Fixes
- Mapping administration – Disabled creation of mappings when the application is locked (NeobeeFrontendSettings v1.0.176).
- Mapping update logic – Mapping updates are now executed using the record ID instead of the previous mechanism (MoProcess v3.58.7, NeobeeFrontendSettings v1.0.175, NeobeeFrontendProject v1.0.123).
- Entity filtering in mappings – Corrected filtering so that only entities from the current application or system entities (without app_instance_id) are displayed (MoUser v3.58.1, MoProcess v3.58.7, MoCentralFrontend v1.0.268, NeobeeFrontendSettings v1.0.175, NeobeeFrontendProject v1.0.123).
- Permission validation – Permission checks no longer incorrectly depend on app_instance_id in permission scheme items (MoProcess v3.58.7).
- Project page access – Access to the project page is now disabled when isAppModelEnabled=true(MoCentralFrontend v1.0.267).
- Dropdown component (multiple mode) – Fixed rendering issue when the dropdown is disabled, in multiple selection mode and without a value (MoCentralFrontend v1.0.271, NeobeeFrontendSettings v1.0.179, NeobeeFrontendProject v1.0.125, NeobeeFrontendCentral v1.0.102).
- AppDashboard dropdown behavior – Fixed paste behavior to ensure consistent entity lookup without converting spaces into commas (MoCentralFrontend v1.0.273, NeobeeFrontendSettings v1.0.105).
- AppDashboard startup page detection – Fixed dynamic detection of the initial page when AppDashboard entries exist in the menu (NeobeeFrontendCentral v1.0.106)
### Improvements
- Mapping configuration UI – Field Opis is no longer mandatory; the field is renamed to Naziv, and when left empty the mapping type is automatically used as the name (NeobeeFrontendSettings v1.0.175, NeobeeFrontendProject v1.0.123).
- Mapping administration – Added display of the target entity name referenced by the mapping (MoProcess v3.58.8, NeobeeFrontendSettings v1.0.178, NeobeeFrontendProject v1.0.124, MoCentralFrontend v1.0.269).
- Permission scheme administration – Added display of permission scheme names in the administration view (NeobeeFrontendSettings v1.0.177).
- Post function validation – Improved validation and error feedback when saving post functions to clearly indicate invalid fields in the root function configuration (MoCentralFrontend v1.0.272, NeobeeFrontendSettings v1.0.180, NeobeeFrontendProject v1.0.126, NeobeeFrontendCentral v1.0.103).
- Tickets page – authorizations UI – Authorization section is hidden when no project is selected (MoCentralFrontend v1.0.276).
- NeobeeUI library – Additional business UI components migrated to the centralized NeobeeUI package (NeobeeFrontendCentral v1.0.106, NeobeeFrontendProject v1.0.128, NeobeeFrontendSettings v1.0.182).
### New Features
- Tickets page – delegations / authorizations – Initial implementation of the UI and authorization logic for displaying tickets to delegated users (MoCentralFrontend v1.0.275).
## February, week IV
### Fixes
- Fixed permission schema listing to correctly display only active schemas (MoCentralFrontend v1.0.265, NeobeeAdminTenantFrontend v1.0.167).
- Fixed permission validation logic by extending checkProcessPermission to also validate app_instance_id, ensuring correct permission scoping beyond map_reference (MoProcess v3.58.5).
- Fixed application selection during user group creation by removing the mandatory application requirement (NeobeeFrontendSettings v1.0.171).
- Fixed missing toast notifications after custom table import actions (success and failure states).
- Fixed App and App Instance administration where name and description fields were not persisted during update operations, and added an icon column to administration tables.
## February, week III
### Fixes
- Improved the Custom Tables administration UI by preventing column deletion when only one column remains, fixing primary key selection when the primary column is removed, disabling unselecting of the primary column, automatically setting the column type to text when adding a new column, and applying the same logic consistently across TABLE, VIEW, and PROCEDURE types.
### Improvements
- Extended the Infrastructure Limits page with support for displaying inactive records and implemented full CRUD operations.
- Enhanced Tab component to support inline rendering of additional UI elements alongside tab headers, reducing unnecessary empty space between tabs and page content.
- Added support in Select form components to display ext_code or id in dev data based on the VUE_APP_TEMP_MAP_SELECT_KEY_TO_EXT_CODE environment variable.
### New Features
- Completed implementation of Custom Tables – VIEW type, including full CRUD support and correct handling of configuration changes with conditional creation and removal of physical tables and views.
## February, week II
### Fixes
- Fixed float field handling in EU number format, preventing value corruption when entering invalid decimal precision (MoCentralFrontend v1.0.258, NeobeeFrontendSettings v1.0.152, NeobeeFrontendProject v1.0.107, NeobeeFrontendCentral v1.0.81).
- Fixed horizontal scrollbar visibility in App Dashboard issue list.
### Improvements
- Optimized file opening and downloading to always load the latest file version when opening or editing in OnlyOffice (MoCentralFrontend v1.0.252, MoProcess v3.56.16).
- Enhanced file templates download by introducing a new action that supports file_data column handling (MoCentralFrontend v1.0.253, NeobeeFrontendSettings v1.0.147).
- Added JSON formatting configuration for AdvancedTable components, aligned with AppDashboard behavior (MoCentralFrontend v1.0.256).
- Introduced configurable float number formatting to remove trailing zeros (MoCentralFrontend v1.0.258, NeobeeFrontendSettings v1.0.152, NeobeeFrontendProject v1.0.107, NeobeeFrontendCentral v1.0.81).
- Improved AppMapPicker behavior to correctly respect is_edit_enabled and app_is_locked settings (MoCentralFrontend v1.0.260, NeobeeFrontendSettings v1.0.154, NeobeeFrontendProject v1.0.109, NeobeeFrontendCentral v1.0.83).
### New Features
- Introduced Remote Points Interface with REST endpoint / process function integration, including endpoint selection restricted to endpoint types implementing the required interface (MoProcess v3.56.20, NeobeeBase v3.56.1, MoCentralFrontend v1.0.255, NeobeeFrontendSettings v1.0.149, NeobeeFrontendProject v1.0.104).
- Added logging on form component creation, storing creator user and creation timestamp (MoCat v3.56.2).
- Added frontend application version display (MoCentralFrontend v1.0.259, NeobeeFrontendSettings v1.0.153, NeobeeFrontendProject v1.0.108, NeobeeFrontendCentral v1.0.82).
- Enabled selection of inactive users on forms (MoCentralFrontend v1.0.261, NeobeeFrontendSettings v1.0.155, NeobeeFrontendProject v1.0.110, NeobeeFrontendCentral v1.0.84).
- Implemented Custom Tables – VIEW type, including CRUD support and physical DB view creation/update (CREATE OR REPLACE).
- Prepared the Infrastructure Limits page, including validation logic and a delete confirmation popup.
## February, week I
### Fixes
- Project matrix component – Fixed crashes when toggling editability, visibility, and mandatory flags (NeobeeFrontendProject v1.0.99).
- Components administration – Fixed improper form reset behavior when switching custom tables, which caused stale data to remain in memory and validation to fail. The form is now fully re-rendered on table change (NeobeeFrontendSettings v1.0.145, NeobeeFrontendProject v1.0.102, NeobeeFrontendCentral v1.0.77).
- AppDashboard table – Fixed text alignment issues when column text is truncated to a fixed character limit.
- Application ext_code validation – Added frontend and backend validation to allow only lowercase letters and numbers.
- Process diagrams – state coordinates – Fixed missing state coordinates during project creation by automatically assigning coordinates to all states. This prevents diagram corruption and ensures correct rendering on target systems.
### Improvements
- PDF preview – Added native browser-based PDF preview as a replacement for OnlyOffice when viewing PDF files. OnlyOffice remains in use for document editing and other Office formats when available (MoCentralFrontend v1.0.249, MoProcess v3.56.5).
- AppDashboard – Dropdown search – Added support for disabling ASCII conversion during search (MoCentralFrontend v1.0.238, NeobeeFrontendCentral v1.0.70).
- Base API routing (cloud) – Extended API routing logic previously available on on-prem to cloud environments for dashboard, endpoint, knowledge, notification, and calendar APIs. All frontends now route these APIs exclusively through the base stack (MoCentralFrontend v1.0.239, NeobeeFrontendCentral v1.0.71, NeobeeFrontendProject v1.0.98, NeobeeFrontendSettings v1.0.142).
- AppDashboard – table column mapping – Added support for mapping table columns to fields in CREATE_ISSUE actions.
Issue list filters (backend) – Added support for filtering ticket fields of type data / custom table with multiple cardinality. Previously, filters only supported single-value fields (MoProcess v3.56.4).
- Application export – Implemented detection and conversion of file template references on POST functions into NRN format (MoProcess v3.56.11).
### New Features
- AppDashboard – IssueStateFilter – Introduced a new component type used for filtering IssueList components by issue states (MoCentralFrontend v1.0.238, NeobeeFrontendCentral v1.0.70).
- Application export – Added support for exporting es_process_file_template.file_data (LONG_BLOB) as a Base64-encoded string (MoProcess v3.56.8).
## January, week IV
### Fixes
- Endpoint administration – Fixed missing dynamic fields when creating records in the es_endpoint table and aligned endpoint type definitions with naming conventions (values to values_list) (NeobeeFrontendSettings v1.0.137).
- AppDashboard – Fixed issues related to tables configured with external_value settings that were introduced during migration (NeobeeFrontendCentral v1.0.65).
- App map editability – Fixed handling of es_app_map.is_edit_enabled for installed applications, ensuring that mappings cannot be modified when editing is disabled. Additional optimizations were applied to application administration pages to reduce unnecessary server requests (MoCentralFrontend v1.0.235, NeobeeFrontendSettings v1.0.140, NeobeeFrontendProject v1.0.97, NeobeeFrontendCentral v1.0.68).
- ProcessDataModal – Improved UI behavior and usability by removing obsolete conditions for opening processStateModal, fixing table scrollbar rendering issues, and updating the Errors tab to remove redundant columns and add an action button for opening a detailed error popup. The Monitoring Errors view was extended with additional state-related information.
- Alert component – Fixed CSS padding issues.
### Improvements
- /neobee/api/base routing – Introduced a mechanism for permanent and temporary API mappings under /neobee/api/base. Permanently mapped APIs no longer depend on the VUE_APP_NEOBEE_API_BASE_ENABLED environment flag, while temporarily mapped APIs still rely on it.
- GitHub Actions / frontend utilities – Established a complete development flow for the frontend eutil library, covering cloud, on-prem token stored in secrets, and local development via CLI. The estehdev/eutil library was integrated into additional frontend projects, providing a basis for extracting shared code into installable libraries and reducing manual code synchronization (NeobeeFrontendSettings v1.0.138, NeobeeFrontendProject v1.0.96).
- Select component (forms) – Continued UX refinement, including upcoming support for removing trailing zeros from float values.
## January, week III
### Fixes
- On-prem file download – Fixed incorrect filename handling during file downloads, which previously resulted in invalid or meaningless file names.
- Linked URL component – Fixed edge cases related to URL persistence and improved rendering of excessively long links (MoProcess v3.55.7, MoCentralFrontend v1.0.227).
- Project administration – App model references – Fixed UI refresh issues when removing SMTP references or permission scheme (NeobeeFrontendProject v1.0.90).
- Process function copy – Fixed incorrect app_instance_id assignment during process function duplication (MoProcess v3.55.8).
- Custom tables – Improved duplicate record handling by displaying a specific validation message instead of a generic error.
- Endpoints administration – Fixed “Active only” filter behavior for remote endpoints.
- Monitoring / UI styling – Fixed CSS issues in AppDashboardMenu related to navigation text rendering.
### Improvements
- Linked URL component – Enabled external value assignment through form actions (MoCentralFrontend v1.0.226).
- Issue List Filters – Extended filtering support to multiple user fields. Previously, filtering was limited to single-value fields; user fields are the first to support multi-value filtering (MoProcess v3.55.1).
- Form Select component – Introduced a new rendering mechanism for disabled dropdowns, displaying static text instead of relying on the default vueselect disabled behavior (MoCentralFrontend v1.0.230, NeobeeFrontendSettings v1.0.134, NeobeeFrontendProject v1.0.93).
### New Features
- AppDashboard – Issue List Filters – Implemented filtering mechanism for issue_list components, with support for boolean fields and custom table fields via AppDashboard radio and dropdown components (MoCentralFrontend v1.0.223).
- AppDashboard – Ticket creation parameter mapping – Added a new global parameter mapping type location_url, providing the current web location at the moment of action execution (MoCentralFrontend v1.0.225).
## January, week II
### Fixes
- AppDashboardTable – Added row count display and table pagination (MoCentralFrontend v1.0.206).
- DashboardStatistic component – Introduced a new AppDashboard component for analyzing dashboard access logs, with support for multiple aggregation modes (global, per user, per dashboard, and custom grouping based on log data) (MoCentralFrontend v1.0.214, MoDashboard v3.53.2).
- Remote Repository support – Implemented build, publish, and combined build & publish operations for remote repositories (NeobeeFrontendSettings v1.0.121, MoProcess v3.53.37).
- NeoBee API base prefix – Added support for /neobee/api/base prefix in on-prem deployments for calendar, notification, knowledge, and endpoint APIs (MoCentralFrontend v1.0.218, NeobeeFrontendSettings v1.0.122, NeobeeFrontendProject v1.0.89, NeobeeFrontendCentral v1.0.53).
- App Instance Picker component – Introduced and integrated across relevant pages, with contextual filtering based on selected application and appModel state.
- ProcessDataModal – Added a new Errors tab and improved navigation to related tickets.
### Improvements
- AppDashboard – Improved parameter mapping during ticket creation, enabling transfer of dashboard URL parameters.
- Applications – Disabled upload, download, and build actions when the application is not on a development system (NeobeeFrontendSettings v1.0.118).
- Custom Tables – Relaxed application selection criteria, allowing visibility of locked applications (excluding neobeeutil) (MoCentralFrontend v1.0.217, NeobeeFrontendSettings v1.0.120, MoProcess v3.53.25).
- AppDashboardTable – File operations – Improved error handling when process files or process_instance_idare missing (MoCentralFrontend v1.0.217).
- Export functionality – Included process custom table records in export flow and added error handling for tables undergoing migration, with user-friendly UI messages (MoProcess v3.53.28, NeobeeFrontendSettings v1.0.123).
- AppDashboardTable – Added support for URL-formatted columns (clickable links) and global search across all columns.
### New Features
- Form Matrix – Stabilized behavior by refactoring and applying a potential fix (NeobeeFrontendProject v1.0.83).
- Float input handling – Fixed incorrect formatting on focusout events and corrected validation to properly enforce decimal minimum values (e.g. 0.01, zero no longer allowed) (MoCentralFrontend v1.0.205 / v1.0.210, NeobeeFrontendProject v1.0.84, NeobeeFrontendSettings v1.0.112, NeobeeFrontendCentral v1.0.50).
- Date component configuration – Fixed invalid validation of default time fields (NeobeeFrontendSettings v1.0.113, NeobeeFrontendProject v1.0.86).
Administration – Custom table components – Fixed errors when components referenced non-existent custom tables (MoCentralFrontend v1.0.215, NeobeeFrontendSettings v1.0.116, NeobeeFrontendProject v1.0.87).
- AppDashboardTable export – Prevented export failures caused by invalid JSON values requiring formatting (MoProcess v3.53.20).
## January, week I
### Fixes
- AppDashboard - Removed ineffective Process filter in My Approvals and My Requests modes.
- AppDashboard - Fixed tooltip rendering by properly formatting JSON fields.
- AppDashboard - Fixed radio button component emitting empty default values.
- Fixed Multiple Select search input layout issue when multiple options are selected.
- Fixed form refresh and validation issues when changing component types in Settings.
- Fixed stale application selection displayed after closing custom table creation popup.
- Fixed duplicate developer validation by code.
- Fixed direct app instance installation from file (reinstallation now possible and version visible).
- Fixed table copy incorrectly requiring application selection in certain scenarios.
### Improvements
- Table & Entity Copying - Extended file template copy mechanism to table copying. Restricted sensitive fields from JSON input and moved them to explicit UI selection (e.g. Application, Endpoint for remote tables). Added copy support to REST endpoint pages with server-side copy logic. (MoCentralFrontend v1.0.185, NeobeeFrontendSettings v1.0.97, MoCentralFrontend v1.0.190, NeobeeFrontendSettings v1.0.98)
- Project Configuration - Removed Single State Mode setting from UI; value is now set only on creation and cannot be modified afterward (MoCentralFrontend v1.0.188, NeobeeFrontendProject v1.0.79, MoProcess v3.52.14).
- AppDashboard dropdown search extended to visible columns and filter_search support added (MoCentralFrontend v1.0.197, v1.0.202).
- AppDashboard table improvements in vertical mode, including per-column text wrapping configuration and improved default wrapping behavior (MoCentralFrontend v1.0.203).
- Iframe Handling - Automatic noMenu=1 parameter added to iframe URLs on AppDashboard (MoCentralFrontend v1.0.188).
- Added system only filter for permission schemes, form schemes, and resolutions. Introduced extended developer view for permission schemes.
### New Features
- AppDashboard – Implemented event logging mechanism for AppDashboard pages, including page open events (open_dashboard)  (MoDashboard v3.52.5, MoCentralFrontend v1.0.187). 
- App Store – Enabled creation of remote repositories and listing applications from remote repos. Replaced Install button with Installed label. Removed Issued by field for cleaner UI (NeobeeFrontendSettings v1.0.105, MoProcess v3.53.6).
- Introduced reusable App Instance Picker component.
