# NeoBee Releases 2025
## October, week IV
### Fixes
- Subform Execution – Verified and tested improved subform save logic when containing EXECUTE_FUNCTION and “Set value” filters.
- Approval Deadline Requirement – Fixed a frontend issue causing execution errors when opening state details (MoCentralFrontend v1.0.100).
### Improvements
- App Export/Import – Enhanced export/import functionality to support proper handling of form components, REST endpoint definitions, and app developer metadata. The NRN generation logic was updated to work with appInstanceId.
### New Features
- State Management – Updated the default behavior for auto insert transitions and state category when creating new states. The default values are now: Auto insert transitions: off (2) and State category: INPROGRESS.
## October, week III
### Fixes
- JS eval loop on multi-form tickets – fixed infinite loop occurring when evaluated results were written back to the same triggering field (on value update → js eval → change value → on value update). Added restriction to prevent selecting the same element as a target.
- Comment submission on tickets – fixed issue where draft comments with attachments were visible to other users, allowing them to post under another user’s name. Draft reuse mechanism removed; a new draft is now created for each comment session. (MoProcess v3.43.2, MoCentralFrontend v1.0.94)
- Action execution in subforms – resolved cases where subforms with actions (e.g. dropdowns using “Set value” filters) lost field values after saving. Added recursive detection of delayed changes and improved handling of parallel executions. Implemented prevention of duplicate “cat item” entries from AdvancedTable components.
### Improvements
- MoCentral – Process State Modal – added validation ensuring that approval state changes are allowed only if at least one of the fields is selected.
- Neobee Util – adjusted money-to-text conversion so that generated text starts with a lowercase letter.
### New Features
- SQL View Designer – reactivated development of the SQL View Designer module. Implemented a new canvas foundation inspired by railway.com, allowing tables to be visually connected and manipulated. Added column selection via checkboxes and visual linking between columns (including within the same table). Lines now automatically position depending on table placement. Introduced UUID generation for custom table columns and improved interaction feedback (highlight on selection, dynamic link line).
- Remote Endpoint Types – added new admin pages Endpoints and Endpoint Types, enabling the creation of endpoint types beyond predefined ones. Each endpoint type includes name, definition, and application; each endpoint includes name, description, type, secret, and definition. ext_code is generated automatically for both entities.
## October, week II
### Fixes
- App Export – removed the column es_process_definition.default_start_state_id from the export and dev database (it existed only on the dev environment and caused production errors).
- Application Store – fixed an issue loading build details from remote repositories; corrected labels and minor visual bugs; aligned readonly fields with static display.
- Application Store - Read-only fields now displayed as static text for better clarity.
- Application Store - Field length alignment with database schema (name/ext_code: 1024, description/release notes: 65535).
### Improvements
- REST Endpoints – added the option to select an Application when creating REST endpoints, along with export/import support between applications.
- Approval Process – improved behavior when canceling ticket creation; the process is now properly canceled if the user aborts form filling. Improved behavior during voting – if the user cancels while creating a ticket, the vote submission is now also canceled. MoCentralFrontend v1.0.89.
- Application Store - Added is_installed and is_build_published flags in server actions for listing and retrieving app details, allowing the frontend to detect whether an app is already installed and whether installation is available (depends on a published build).
- Application Store - Automatic generation of ext_code from name across all administration pages.
- Application Store - UI improvements: added description field, redesigned build details section (expandable menu on the right side of the table), harmonized font sizes, colors, and shadows, and clarified the “Publish” button functionality.
### New Features
- Loop States – implemented a new Loop state type with full UI support and operations for creating and maintaining transitions. The necessary state_type is automatically created (if it doesn’t exist). Introduced new action_type (6, LOOP). MoProcess v3.42.5, MoCentralFrontend v1.0.91.
- Developed a local RAG system - Loads and parses a PDF document, splits it into semantic chunks, and stores them in an Infinispan in-memory vector database. The system retrieves relevant text chunks based on user queries and generates contextual answers using Ollama.
## October, week I
### Fixes
- Project Creation – Fixed issue when creating a project without selecting an application (MoProcess v3.41.1).
- Tasks Page – Fixed a frontend issue that occasionally occurred when selecting the “Single project” filter and opening the state dropdown (causing endless loading) (MoCentralFrontend v1.0.80).
### Improvements
- ADD_TO_LIST – Added implicit support for inserting one list into another (previously only single items could be pushed). Added type detection and duplicate control (MoCentralFrontend v1.0.66).
- Form Cascade – Updated the icon for selecting a single level from “+” to a right arrow (MoCentralFrontend v1.0.74).
- moCentral - Chat – Increased maxlength for chat messages to 1024 characters in LlmChat.
- moCentral - Chat - Created new neoChatPage component and integrated it into the Diagram page.
- moCentral - Chat - In neoChatInput, added yellow focus border and bee icon animation.
- moCentral - Chat - Added removeMessageDots method to clear loading dots after 2 minutes if no response is received.
### New Features
- App Store/Repository – Defined the structure and distinction between repositories (for builds) and app stores (for installation and download).
- App Store/Repository - Implemented operations for reading and managing both App Store and Repository, including fetching remote repo info, listing apps and builds, retrieving app details, installation, and download.
- App Store/Repository – Repositories can now be local or remote, with App Store actions automatically handling whether the operation runs locally or via HTTP.
Added a new definition column to the es_app table (enabling icon display in installations).
- LLM Integration – Established frontend-to-Ollama server communication and enabled two-way message exchange via notifications.
- LLM Integration – Created MCP client and multiple Tool operations for: creating/deleting process states, creating transitions, searching and editing tickets
- LLM Integration – Implemented and tested tools for adding, modifying, and searching tickets.
- ID Reader / Document Scanning – Completed full document scanning workflow: Enabled uploading multiple files per operation, automatically creating records in es_apptool_event_attachment and implemented file transfer from attachment to processfile bucket, making them active attachments on the related ticket.
## September, week V
### Fixes
- JSON Data Input Component – fixed issue where key disappeared from UI when value was deleted (MoCentralFrontend v1.0.60).
- Application Administration (Labels) – corrected wrong labels on popup (MoCentralFrontend v1.0.59).
- Custom Tables – fixed bug with incorrect handling of optional app_instance_id parameter during table creation (MoProcess v3.40.1).
- Mapping Display – resolved frontend issue when opening mapping pages in applications (MoCentralFrontend v1.0.63).
### Improvements
- State Modal Defaults – disabled automatic “insert transitions for all states” option; set IN PROGRESS as the default state type.
### New Features
- Application Model (Translations) – implemented application-level translations with UI integration, maintenance, and import/export support (MoCat v39.1, MoCentral v3.39.2, MoCentralFrontend v1.0.61, MoCentral v3.40.3, MoCentralFrontend v1.0.62).
- LLM Integration (Quarkus & MCP) – initial class creation in Process API with MCP annotations for state creation; first successful Java-to-MCP endpoint call enabling two-way communication setup.
- LLM Chat UI – new chat component created (LlmChat, LlmChatMessage) on Diagram page.
- LLM Chat Backend – implemented send_message action with JSON payload via AppSync, Lambda, and REST API; integrated with frontend for real-time communication.
- ID Card Reader & Scanning – infrastructure for reading personal ID cards established, including event logging (es_apptool_event), Base62 link generation, result endpoint, GraphQL notifications, and orchestration of form actions.
## September, week IV
### Fixes
- Application Model – fixed issue with setting app_instance_id on START and CODE states during project creation – MoProcess v3.38.8.
### Improvements
- EXECUTE_FUNCTION action – added support for passing form parameters, previously available only in REST button – MoCentralFrontend v1.0.58.
- Application Model – completed first phase changes to ensure proper propagation of app_instance_id across all verticals of an application (entities created from application/project creation now inherit app_instance_id) – MoCat v3.38.1, MoProcess v3.38.7, MoCentralFrontend v1.0.55.
- VTL Context in multiple subform – enabled VTL evaluation for default context values when adding new rows, replacing previous hardcoded-only option – MoCentralFrontend v1.0.54.
- Post function (system/ticketfindbyfield) – added empty-value validation – MoProcess v3.39.3.
- Post function (system/ticketfindbyfield) – added limit parameter to query (default value: 1000) – MoProcess v3.39.2.
- Date utilities – added DateAddMinutes and DateSubMinutes methods for handling date-time calculations.
### New Features
- App Store / Marketplace – initial data model defined, including first iteration of API specification covering app build, push to store, and publishing.
- Application Model (translations) – defined approach for handling es_lang_item per application, enabling flexible translation management grouped by app_instance_id, with fallback to original resource name if translation is missing.
- Application Model (support) – additional technical clarifications and support provided for handling app_instance_id.
- File parsing post function – added functionality to parse .xml and .csv files within projects.
- MCP (Model Context Protocol) – implemented MCP server with two tools available for AI calls: getTimeInTimeZone – returns current time for a given timezoneId; getJVMInfo – returns Java Virtual Machine system information (number of processors, free, total, and max memory).
- MCP (Model Context Protocol) - implemented MCP client that allows the AI assistant to use existing tools in real time. The client receives user input, communicates with the LLM (local Llama 3.2 model via Ollama), processes queries, and invokes tools from the MCP server accordingly.
## September, week III
### Fixes
- Signers Matrix – fixed issue with integer formatting component (field Amount) incorrectly reporting invalid input.
- Digital signature validation – modified post function to support multiple input files.
### Improvements
- Ticket approvals ("My Approvals") – added filtering by active state instance records to improve performance.
- Application Model – introduced automatic creation of a default permission schema at the application level, linked to the project upon creation.
- Application Model – enabled usage of permission schema via map reference in checks (ISSUE_VIEW, ISSUE_EDIT, get_issue_list), controlled by env parameter APP_MODEL_ENABLED=1.
- bankOcr – DateRange component – allowed selection of the same date for both dateFrom and dateTo.
### New Features
- Application Administration – added display of developer data (id, ext_code, name) on administration pages for Applications, Application Instances, and Developers.
## September, week II
### Improvements
- Form Button Option – Implemented the Allow action when readonly setting, enabling buttons within locked forms/subforms to remain active.
- Adjusted text and barcode position in attachmentAddBarcode to improve visual layout (top margin set to 20pt).
- ## September, week I
### Improvements
- Approval Matrix – Added a permission that allows defined user groups to edit the money range at the column level. The client verifies group membership and shows the edit option only to authorized users.
## August, week IV
### Fixes
- Filter Administration – Fixed issue where the State field was not rendered in central administration, causing its value to be lost when saving filters. Root cause was missing entry in es_form_component table.
- Corrected issues on signer and approval dashboards matrices.
- System Calls – Fixed evaluation of conditions.
- XML Parsing – Adjusted parsing logic, fixed text and barcode rendering issues.
### Improvements
- Approval with Digital Signature – Now consults canSign parameter when user authorization is required.
### New Features
- Digital Signature Validation – Implemented function to validate digital signatures for a given keychain and file object, with supporting lambda and REST endpoint (validate_digital_signatures_new).
## August, week III
### Fixes
- External Links Security - Added rel="noopener noreferrer" to all links with target="_blank" to comply with security report requirements.
- Ticket List – Adjusted sorting logic to use ordinal_no (weight) consistently.
- Fixed issue when sorting by number-type columns.
### Improvements
- Ticket Status Selection (UI): Statuses are now displayed instead of status types in filters.
- Ticket Status Selection (UI): Automatically checks/unchecks related statuses of the same type.
- Ticket Status Selection (UI): Displays translated status names when available, otherwise the original name.
- Ticket Status Selection (UI): Search works by name, code, or type.
- Ticket Sorting - Saving of selected sort order in filters (user preference).
- Certificate Chains & Keystore: Completed update cycle for certificate chains and keystore.
- Signature Validation Function (AWS): Implemented signature validation function for a given keychain and file object. Created corresponding Lambda and REST endpoint.
### New Features
- Ticket Attachments: Enabled file uploads in ticket conversations. A project-level flag controls this option (enabled by default).
- AdvancedTable – User Column: Added implicit support for arrays of users. If the stored value is an array, all users are displayed one below the other.
## August, week II
### Improvements
- Approval Popup UI – improved visual clarity of clicked signals by changing the popup header color, making it easier to distinguish actions.
### New Features
- Proxy on Post Functions – enabled configuration of a “proxy” remote endpoint in post function settings.
- Partial Reconciliation – implemented UI controls for editing an existing vote and submitting a new one; information is now forwarded to the backend logic.
- Certificate Chains & Keystore – added functionalities for managing certificates, certificate chains, and keystores.
## August, week I
### Fixes
- AdvancedTable in Single Subform - Fixed issue where value selection visually disappeared on the UI (although values were saved correctly).
- eval Function – formparent Scope - Bug reported when referencing formparent inside eval, but could not be reproduced.
- AdvancedTable – "Set Value" Filter (Single Mode) - Fixed bug where "Set Value" option didn’t work correctly in single-mode AdvancedTable instances.
- Ticket State Dropdown - Fixed an issue where the dropdown kept expanding indefinitely when clicking multiple times, especially when no available states were present.
- Float Field – EU Number Format - Improved input handling for float fields to support comma-based decimal format (e.g., 1.234.567,89). Internally, values are still saved using dot format (1234567.89).
### Improvements
- Form Component Administration - When switching visuals between components of the same data type, configuration is preserved (currently supported only for date fields).
- Masked Date Input Behavior - Cursor now auto-jumps between day → month → year fields during input, improving UX.
### New Features
- Partial Approval on Tickets - Prototype implemented for partial approval, allowing users to approve individual items where they have permission. Approval controls are shown per item.
- toDatetime Function (Frontend) - Introduced a global utility function for converting barcode-style date strings to server datetime format (250720251001 → 2025-07-25 10:01:00).
- REST – Create User Group – Added REST endpoint to create user groups.
- REST – SFTP PUT/GET – Added REST endpoints.
- REST – Parse Attachments – Added REST endpoint to parse attachments using a predefined configuration.
- REST – DataSet Save Full Row – Added option in DataSet REST calls to save the entire row (data_map) for a table.
- Added support for setting cutoffTime dynamically in state.
- Approval Notification Template Editing – Added the ability to modify the notification template for approvals.
- VTL – daysBetween – Added VTL function returning the number of days between two dates.
- VTL – Excel Formula Functions – Added VTL functions for Excel formulas: coupdays, coupdaysnc, and price(library_formula).
- Localized Date-Time Formatting – Changed date-time formatting to Serbian locale (formatDate).
- Windows Share – Save File – Added function to save files to a Windows share and function to retrieve a file from a Windows share only if it has changed.
## July, week V
### Fixes
- Custom Tables - Fixed saving of empty values in number and boolean type columns. Previously, empty numbers couldn't be saved, and false boolean values were not handled correctly.
- Custom Tables - Fixed unnecessary ALTER statements being triggered when modifying columns.
- Custom Tables - Fixed issues with saving individual rows in custom tables.
- Custom Tables - Optimized data loading in custom table settings: now only the selected tables are loaded for many-to-many columns (if such columns exist), instead of loading all tables.
- Subtask Files Header - Fixed text wrapping issues in the file header within subtasks.
### Improvements
- Help Popup - Added support for disabled categories (status ≠ Y) and sorting using ordinal_no.
## July, week IV
### Fixes
- Reports Page – Fixed issue where default "from–to" date range was not applied correctly when selecting a report.
### Improvements
- Help Popup – Improved display of categorized documents: loading spinner now appears locally when expanding/collapsing categories; Hovering over a document highlights all categories it belongs to; Implemented basic document search – narrows the list based on input without loading all categories in advance.
- Custom Tables – Refactored ProcessCustomTable manager, with simultaneous bug fixing and logic cleanup.
### New Features
- Reports Page – Fixed issue where default "from–to" date range was not applied correctly when selecting a report.
## July, week III
### Fixes
- Parent Ticket Display in Subtask - Resolved layout issue when parent ticket had a long name and code.
- Money Field Parsing Issue - Fixed issue with value parsing when repeatedly pressing “Enter”.
- Float Field Exit Behavior - Fixed value parsing error when leaving the input field.
- EXECUTE_FUNCTION: Fixed problem with adding multiple EXECUTE_FUNCTION actions to the same event.
- Linked Task Icon Consistency: Standardized icon color (orange) for opening tickets in a new tab across both simple and standard modes.
### Improvements
- File Upload Section - File list now refreshes automatically when ticket transitions to a state of type “STATE” (not “CODE”).
- Decimal/Money/Float Field Validation - Minimum and maximum values now support decimals. Decimal precision is controlled via the “Max decimal places” setting.
- Subtask Live Refresh - Subtask states now update live on the parent task detail view.
- Form Field Admin – Auto-scroll: Admin UI now auto-scrolls to the visual position of the edited component.
- Field Value Save Order - Field values are now saved before executing defined actions, reversing the previous logic.
- Help Popup Categorization - Backend and frontend work done to support categorization of help documents, enabling support for more than three categories.
### New Features
- Report Generator – User Settings Integration - Added support for applying user-specific values to reports that use forms for field display. User settings are applied last, after all filters.
- Ticket Creation Look & Feel Config - Added configuration for displaying the "Create Ticket" popup button on Backlog, Sprint, and Ticket/Task pages. Visible by default; can be hidden via appearance settings.
- Advanced Table - Initial version of the new layout implemented, with available options displayed on the left and selected values on the right.
- Linked Tasks - Implemented a simplified display mode for the linked tasks form component, with fixed relation type and read-only ticket details.
## July, week II
### Fixes
- Fixed an issue where part of the form was re-rendered during state validation, causing the validation process to fail.
- Fixed a bug with group picker components that used the dynamic "Group Prefix" filter, which previously did not function as expected.
### Improvements
- Form Actions – Added validation for value formats in form actions (set, set_fixed, eval). If the value is invalid (e.g. non-JSON for a JSON field), the action is skipped and a console log is written with the field code and problematic value.
- User Preferences – Preferences are now stored server-side (es_ruser_data.preferences), making them available across different user sessions.
- Central File Upload – The form.file_attachment.visible property can now be used to control the visibility of the central file upload area.
- App Dashboard - Added configuration for setting max image width/height in dashboard content blocks.
### New Features
- Subtasks - Subtasks now show the full hierarchy of parent tickets above them (not just the immediate parent). Parent tickets can be visually collapsed.
- User Preferences– User-defined preference values can now be displayed in the form footer via layout configuration using ${field.data.column} notation.
## July, week I
### Fixes
- Subform Cascading Dropdown - Fixed an issue where cascading fields in single subforms lost their display values when the main form triggered a re-render.
- Custom Table Migration Bug - Resolved a bug where migration scripts saved the original table name instead of the updated one.
### Improvements
- Forms for Reports - When creating a form for report field display, it is now auto-checked as a report form by default.
- Form Transition Logic - Values in transition forms are now saved only after clicking “OK”, instead of immediate write to ticket.
- CURRENT_USER Filter - Extended to support multiple-user fields.
- Util - New methods in LibraryDateTool for adding/removing hours from dates.
### New Features
- Dynamic Filters - Added support for dynamic filtering on Assignee and Reporter components, enabling user list restriction by project-linked groups; Introduced new role_list filter to check user roles per project, and improved group_list filter using ext_code.
## June, week IV
### Fixes
- Ticket Filters: Fixed issue when custom table key was not properly mapped in filters.
### Improvements
- Enabled direct form creation from the Reports admin page.
- Attachments on Tickets - Now shows empty table when no files are attached.
- Subtask UI - Improved distinction between ticket name and status.
- Ticket Logs - Added popup support for transition actions in log view.
- Form Datepicker - Added support for relative day-only input.
- Unified icon display for tickets and files without data classification.
### New Features
- Enabled text-based search on user-defined fields in Tasks.
- Added CONTAINS filter for column-level search in Tickets, including support for complex data types.
## June, week III
### Fixes
- Fixed layout issue on the user details card where long content caused overflow across the screen.
- Resolved bug with license update action where name parameter couldn’t be changed.
- Fixed an issue in permission details (onChangeGrantTo method) related to role assignment logic.
- Fixed an issue with license name updates in the License page.
### Improvements
- Refined cross-project ticket creation from approval workflows: the form opens before sending the approve/reject signal, and modified mapped comments are preserved and sent correctly.
- Signal dispatch is now delayed until the popup is closed, regardless of whether the ticket is created.
- Added support for formParent scope in JavaScript expression evaluation on forms.
- Continued work on report module: improved report query logic and sorting; improvements pending deployment.
- On the moCentral project, added validation to the Modules page and.
- In the admin frontend, improved the showErrorToast method.
### New Features
- Implemented field validation for ticket creation from the user settings form, showing a warning when entered values differ from explicitly required ones.
- Enabled evaluation of mathematical and JavaScript expressions within form actions, with results dynamically passed to other fields during execution.
- Enabled classification of process instances (tickets), functioning similarly to file classification.
- Added first version of reports that use a form definition to display a report generator; fields are now rendered based on that definition.
- Developed migration functionality for custom tables, including structural changes to migration_definition, copy functionality with full definition, and upload modal in settings.
- Created number-to-text conversion method with associated documentation.
- Introduced RouterTabs component in the admin frontend.
## June, week II
### Fixes
- Fixed display issues in ticket detail popups opened via direct link.
- Resolved malfunctioning of the IS_VISIBLE filter and confirmed correct behavior.
### Improvements
- Enabled download of uploaded report templates from the report administration page.
- Enhanced get_issue_list to support search functionality across dashboards and subviews (My Approvals, Requests, Team, History).
- Improved visibility logic with the IS_VISIBLE filter for compatibility in multi-form contexts.
- Prepared custom index definitions to persist and replicate automatically during table copy operations.
### New Features
- Added field-level rule indicators in form administration (visibility, required status, conditions, filters, actions).
- Enabled system font switching between Roboto and DINPro.
- Introduced icon-only sidebar navigation mode; currently left menu only.
- Enabled ticket creation in a different project from within approval workflows, with mapped values and system fields.
-Implemented full CRUD for SQL indexes on custom tables, with automatic application during table creation based on stored definitions.

## June, week I
### Fixes
- User Search by Email - Added support for filtering by email address and inclusion of @ in allowed characters.
- Subform Flickering During Input - Partial fix implemented for subform re-rendering issues when dropdowns are opened or data is entered; deeper nesting cases are still under investigation.
- Fixed minor bugs related to vertical tables.
### Improvements
- PROCESS_CUSTOM_TABLE_LIST Query - updated to include filtering by is_remote column.
Custom Table Details Page - two new fields added: Sort Order and Local Copy.
- PDF Merge Utilities: Two new server-side functions for PDF merging (one that fills up to page limit, one that adds whole documents unless it would exceed page count limit) and new action attachment_merge_pdf developed and functional: successfully stores the merged PDF in the database, UI display pending fix.
- LDAP Synchronization Page - two new fields added: userFilter and defaultRoleId.
### New Features
- Ticket Field Mapping on Transition - implemented support for field value mapping or hardcoded values during ticket creation, works both in pop-up and new tab modes.
- Ticket Confidentiality - introduced support for marking individual tickets as confidential with backend validation and flexible response format
- Form Action - Clear Field on Click - added option to trigger clearing of another field via a button click in forms.
- Global Settings Page - implemented a search feature with keyboard navigation (Enter / Shift+Enter to move, Tab + Enter to select) and dynamic highlighting; auto-expands collapsed categories if a result is found inside.
- App Dashboard Tables - separate settings for rows, columns, and headers (text style, background color, etc.); fixed header and optional row striping: conditional row formatting based on cell values (all types, number/date-specific); visual preview of styling changes; vertical table support added with full feature parity to horizontal tables.
## May, week IV
### Fixes
- Custom Table Filtering by Roles - Introduced granular filtering options using MATCH_ANY and negation logic for table row visibility.
- Custom Table Update Method - Fixed issue in updateCustomTable method on details page.
### Improvements
- App Dashboard Table Enhancements - Conditional row formatting (based on any cell’s value); Configurable text size and column width (pixels or char count); Horizontally table (headers on the left).
- Report Overview - Added visualization of ongoing or failed report generations (red/yellow status highlights); Limited to 15 visible reports; Download button only shown for completed reports.
- Report Monitoring Page - Lists all reports in-progress or failed, with metadata and search functionality.
- Enabled physical renaming of SQL table names and table_name field in definitions.
- Report Type Administration - Added ext_code column to report type admin view.
- Tracing and Metrics - Enabled tracing for item add/return and barcode PDF upload; Displayed performance metrics (document size, number of calls, duration).

### New Features
- App Dashboard – Added support for exporting visible columns from App Dashboard tables to Excel, with value formatting matching the UI (users, groups, date, JSON with display format, etc.).
- App Dashboard - Enabled filtering App Dashboard tables by user's favorite tickets using process_instance_id and a showMyFavorites flag.
- Multi-form Row Duplication - Implemented option to duplicate rows in multi-form components. Can be toggled in admin settings (default: off).
- Conditional Visibility/Editability/Required Filters - CURRENT_USER now supports reference values (formparent.field).
## May, week III
### Fixes
- File saving error - Fixed an issue preventing file uploads from being saved properly.
 - Component spinner bug - Fixed spinner not disappearing when no further items were available for processing.
- Styling fixes for radio buttons and checkboxes - Corrected CSS issues for better alignment and visual consistency.
- Subform flickering on first load - Known issue identified and scheduled for resolution (not yet fixed).
### Improvements
- Custom table management - Added options to create local tables from remote definitions with prefilled CRUD popups. Included a flag to preserve original table names and displayed physical table IDs in detail view.
- Custom filtering optimization - Improved filtering logic in get_issue_list using optimized JOIN operations.
- Upload modal improvements - Added a new tab for easier access to table-related data in the upload modal.
- New form condition: UserIsInUserField - Added a condition to check if the current user appears in a specific user field.
### New Features
- Granular permissions for files and form components - Introduced fine-grained access control with support for view, edit, delete, and metadata updates. Permissions can be based on user roles, ticket assignment, or values in custom fields. A new admin UI and CRUD functionality were added. Permission evaluation occurs client-side using live form data.
- Extended matrix for component permissions - Enabled extended matrix mode to set permissions directly on form fields. Permissions on files override all other levels and apply to file instances wherever displayed.
- Custom table filtering by ticket ID - Enabled filtering of custom tables based on the column containing the ticket ID.
- Approval comment control - Added support for per-response-type settings (Approve/Reject/Ignore) to trigger comment popups during approval actions.
## May, week II
### Fixes
- User field loading on forms - User details are now loaded regardless of active/inactive status. User lists still default to active users only, with optional parameter to include inactive ones.
- Ticket status color coding - Investigated inconsistent color application for statuses.
ZIP export duplicate file handling - Fixed issue with duplicate file names during ZIP export by appending suffixes (_1, _2, etc.).
- File classification bugs - Multiple fixes related to validation, popups, and user interactions during file upload with mandatory classification enabled.
### Improvements
- Direct Homepage routing - Implemented support for URL-based navigation using homepage (ext_code) or homepageId (ID). Automatically overrides local storage settings.
- App Dashboard date filters - Integrated external value system and expanded date filtering to support range-based queries (from / to dates); Added support for filter_search events for table filtering.
- API Monitoring - Added "build time" column to the API monitoring table.
- File table on tickets - Simplified displayed columns; Added info button to show file creation date and file size on hover.
- App Dashboard visual styling - Background, text, border, and font-weight customization at the table, column, row, and header levels; Implemented fixed headers and floating component titles for easier navigation; Improved horizontal scrolling placement.
- Mandatory file classification on tickets - Added project-level parameter to enforce file classification on upload; Implemented warning popup if classification is required but not provided.
- New transition condition isDataClassifiedAll - Added transition rule to check if all files on a ticket have assigned classification.
- Rich Text Editor - Added new "Clear All" (X) button to fully clear text; Adjusted previous X button behavior to only exit bullet/numbered lists.
### New Features
- New filter operators in custom tables - Support added for <, <=, >, and >= operators in custom table filters.
- Homepage positioning - Implemented configuration parameter in Look&Feel to position the Homepage above all menu items.
- "Select all" option for ZIP export on tickets - Added functionality to select all files for ZIP export directly.
- User Actions administration - Developed administration interface for managing user actions.
## May, week I
### Fixes
- AppDashboard – Fixed an issue with adding actions to components on the dashboard.
- Validation on Multi Subform – Fixed an issue where required fields inside multi-subform components failed validation when no values were present.
- User Settings local storage – Fixed incorrect loading of other users' settings from local storage.
### Improvements
- AppDashboard external Value - Added support for external values for multiple dropdown components.
- AppDashboard date filtering – Added support for filtering a table using date component values configured in an action.
- Barcode Text Positioning – Enabled positioning text around barcodes on all four sides, and added configuration for barcode size.
- Sortable Table UI – Sort arrows in tables are now positioned to the left of column headers.
- Reconciliation Deadline Display – If the individual deadline differs from the global approval deadline (approve_deadline_global), both values will now be shown.
### New Features
- AppDashboard – Fixed an issue with adding actions to components on the dashboard.
- Validation on Multi Subform – Fixed an issue where required fields inside multi-subform components failed validation when no values were present.
- User Settings local storage – Fixed incorrect loading of other users' settings from local storage.
## April, week V
### Fixes
- Validation on subform-multi subform – Fixed an issue where validation failed if a required field existed inside an empty multi subform.
- User administration-User Settings page – Fixed an issue where E_NULL values were being saved for last_name.
- User settings-local storage – Fixed an issue where user settings from local storage were incorrectly applied across users.
### Improvements
- Enabled detail preview for individual rows in multiple form components when in read-only mode.
### New Features
- AppDashboard-ticket creation from popup – Enabled ticket creation via popup using the existing Home Page selection mechanism.
- Custom table filters-multiple choice dropdown – Enabled filters on custom tables for multiple choice dropdown fields.
- Environment variable for hardcoded sign-in IDs – Introduced env variable VUE_APP_HARD_CODED_ID_FOR_SIGN_IN_FIELDS_ENABLED to optionally fix IDs of username and password fields for sign-in forms.
- X-FRAME-OPTIONS header – Introduced X-FRAME-OPTIONS: DENY header via nginx to improve security.
- Barcode positioning (moattachment project) – Added functionality to position text relative to barcodes on all four sides, and adjustments for barcode size.

## April, week IV
### Fixes
- Special characters in search – Added new special characters (brackets, commas, semicolons) to the ASCII conversion method for dropdown list searches.
- Validation on subform – Fixed issues with inconsistent triggering of validation.
### Improvements
- Project filters on Ticket page – Filters are now placed in a separate section and hidden when no project filters exist.
- Filter display on Ticket page – Simplified the filter list view, focusing on the filter name while keeping actions accessible as needed.
### New Features
- Access rights in AppDashboard table – Restricted table content visibility based on process_instance_id by introducing a JOIN section within the generated get_issue_list query.
- New tab in AppDashboard – Implemented a redirect mechanism for opening files in AppDashboard, supporting existing open_process_file events with flags for popups or new tabs, plus new events view_process_file and download_process_file.
 - Module selection as a configuration – Added a UI option for displaying Process Modules as an auxiliary filter on "Tickets" and "Reports" pages.
- Custom table format "User Group" – Introduced a new option for formatting columns in custom tables.
- AppDashboard - Open in new tab – Enabled AppDashboard opening in a new browser tab via table link actions.
- PDF watermarking – Implemented methods for adding and removing watermarks in PDF documents.
## April, week III
### Fixes
- Parent Filter/Action on Subform - Corrected propagation from parent form to subform.
- Log Popup Scrollbar - Fixed double-scroll issue by adjusting section height
- AdvancedTable Fullscreen Popup - Fixed value transmission and save behavior between main form and popup via OK button
- AdvancedTable Actions Overflow - Fixed action buttons spilling into multiple lines (initial and follow-up fix)
- Queue Item Bulk Action Restriction - Ensured that when "Disable" or "Enable Execution" is selected, the "Apply to all" option is disabled
### Improvements
- Subtask File List on Main Task - Enabled file preview (green hover effect), but disabled editing when viewing files from subtasks
- Ticket Attachment Permissions - Role-based access restriction button hidden
- Translation Export - Labels from approval workflows now included in the export
- Quarkus & Java Upgrade - Upgraded the following apps: MoCompany, MoUser, MoAuth, MoCentral, MoMail, MoCat, NeobeeGraphQL, MoRest2
- Custom Table Sync Optimization - Added batch insert method with upsert (on duplicate key update) functionality to boost sync performance
- ProjectManagementPostFunction Spinner - Fixed validation spinner issue and pushed to production
- Popup Notification for JSON Downloads - Added notification popup for users downloading remote table JSONs (MoCentral)
- Map Field Edit (ProcessFunctionField) - Fixed styling issue where text was overflowing the div
### New Features
- Ticket Page Filters - Implemented classification of filters (multi/single project). In single project mode, filters are visible only when the project is selected and show only that project's state types. Includes admin-side CRUD functionality
- Initial Language at Login - Language selected on the login screen now propagates through the application and is saved as a user parameter
- Project Filters on Ticket Page - Finished UI adjustments and admin operations
- AppDashboard Access Rights - Filter content in the dashboard based on process_instance_id. Uses optional execution of view_custom_table via jsonquery engine
- AppDashboard Column Formatting - Implemented JSON formatting in columns using template syntax like ${field1.field2}, ${field3}
- Default Filter Mapping UI - Componentized the filter mapping selector (like SMTP endpoints). Works with any supported entity type, using app_instance_id
- Export JSON Documents: New export functionality with limits (5,000 for remote, 100,000 for local)
- Custom Table Sync Actions - New action: sync data from one custom table to another, New queue item actions: disable_execution sets dead_letter = 1 for selected IDs only, enable_execution sets dead_letter = null
- Word Watermark Management - Added functionality to insert and remove watermarks in Word documents
- PDF Watermark Management - Added methods to add and remove watermarks from PDFs
- Queue Item Execution Control (UI) - Added "Disable" and "Enable Execution" options; disables "Apply to all" when one of these is selected
- Default Filter Mapping on Projects - Finished mapping logic and applied it on the tickets page. Code merged to master
## April, week II
### Fixes
- Issue with UD ticket creation - Resolved a problem with the subform and file upload where the form remained in a "busy" state due to the flag not resetting. A workaround was provided to bypass the file field during ticket creation
- Ticket List (get_issue_list) filter issue - Fixed casting values in filters that used range mode (from-to) from UNSIGNED to SIGNED. This issue was previously unnoticed
- Login issue - Resolved a problem with loading user settings forms when the user was not logged in, preventing access to the application
- Application of filters and/or actions from parent form in subform - Fixed and ready for deployment
- Scrollbar in popup for logs - Adjusted section heights to prevent dual scrollbars from appearing
### Improvements
- User settings as a filter on the Tickets page - Enabled the use of values from user settings in filters. When a field selection mode from user settings is activated, the system will insert that value into the filter, if it exists
- Filter operator "not_equals" - Added a new filter/SQL operator for custom table filters
- Default values on form per user - Implemented a mechanism to set default values at the user level, stored in local storage
- Digital signature mode selection - Implemented a setting to determine whether the digital signature mode selection is available. Default is disabled, and the system automatically attempts to open the local desktop application
- File List with subtasks on main task - Enabled file preview for subtasks similar to main ticket files (green field on hover). Editing is disabled in this mode
### New Features
- Float type - Implemented a new subtype for data_type=number. It is stored as a string with a decimal point in the database and rendered on the client side based on component configuration. Supported in ticket filters
- Default values - Added functionality for default values on forms at the user level
- Selection mode for digital signing - A setting was added for toggling the selection mode for digital signing
- Mapping - Added automatic assignment of app_instance_id to forms and components, and created a UI to restrict component selection based on the presence of app_instance_id
- Ticket type - Added a "group type" option in ticket type administration that can only be changed at creation time
- Export functionalities - Implemented JSON document export with a limit of 5000 for remote tables and 100000 for local ones. Added actions for exporting to Excel (exportToExcel) and for synchronizing data between custom tables
- User Notification for Export Actions - Added pop-up notifications for users when downloading Excel for remote tables, alerting them of any limitations
## April, week I
### Fixes
- App Dashboard bug fix - corrected the behavior of the popup for file previews from the table
- AdvancedTable bug fix - removed the coloring of rows blue when a row is checked if the component is in readonly mode, as established in a meeting
- Custom table selection bug fix - added statusId=1 parameter in several requests, so inactive tables are not visible when selecting
- Corrected issues with ticket creation due to subform rules with files; the refresh was not resetting whether the component was loaded, leaving it in "busy" state.
### Improvements
- App Dashboard internal state + URL - working on a mechanism for saving dashboard state in a JSON space, and linking the URL to that state
- Improvements in Action functionality on the AdvancedTable component - introduced the source_type parameter for mapping within one action, with possible values "column" (referring to a column from the custom table) and "plainvalue" (exact/hardcoded value)
- Various updates, including the deletion of mp4 files from the frontend application
- Central space listening for fields, with optional JSONPath for listening: field.subfield1.subfield2
- Action for writing to the central space and transformations, with key and value combinations applicable
- Improvements in mapping: Added app_instance id in CRUD operations for filters, user groups, and project roles, Added automatic insertion of app_instance_id from the backend during project creation, issue type addition, and state creation. Continuing the automation of adding app_instance_id to entities with a field for selecting the application instance where necessary
### New Features
- Added a new feature for linking to a document, which includes a new route for displaying the details of a single document without showing the "space" and ticket (/document/content/$documentRootId)
- Improved functionality in App Dashboard - enabled the use of filter_search event for filtering content of another table through its value event and EMIT_EVENT mechanism in action
- Enhancement in the Form functionality - reduced the vertical spacing between fields on the form by 30%
- App Dashboard internal state - model revised so that components retain their state but can react to a specific subscription type from the app dashboard's external space. Minor issues being resolved for a working version tomorrow
## March, week IV
### Fixes
- Template Mapping: Fixed an issue where logic worked locally but failed in the cloud environment
### New Features
- Actions on AdvancedTable component type: Implemented an action system for the AdvancedTable component. It now allows a button click to open a form from the homepage and map values from the clicked row to the form’s initial values
- Document Link functionality: Added a new route to display details of a single document without showing its "space" and tickets
- Endpoint: /document/content/$documentRootId
- Hidden Pages on Homepage: Added is_visible support for homepage pages. Pages are visible by default but can be hidden while still being accessible via direct URL
- Automatic mapping during file template creation: Displayed the app instance each template belongs to, Added 3 switches on template creation: Auto-create mapping (default: true), Allow mapping edits (default: true), Allow mapping export (default: false). Options are visible only when an app instance is selected
- Project Roles Configuration Page: Added ProcessDevData component to display extra data (e.g., id, ext_code) for project roles
### Improvements
- TransferOrder Component: Improved validation for the payment model. On the Statistics page, added a new column "Branch Office" to the order table
- AdvancedTable UX: Actions column is now pinned to the right side, no need to scroll horizontally to access it
- App Dashboard Filtering: Enabled use of the filter_search event to filter another table’s content via its value event and the EMIT_EVENT mechanism
- Form Layout: Reduced vertical spacing between fields by 30%
- Calendar Enhancements: Added a definition column to es_calendar to support: Time zones (default fallback to tenant setting), 
Workdays (mon–sun), Working hours (stored in UTC, displayed in calendar's time zone), Breaks & holidays (datetime from / to, with description; stored as 00:00–23:59), Per-day work hours & break definitions (UI implementation in progress)
- TransitionModal Component: In the "Conditions" tab, added UserIsInGroupField and extended methods for adding/editing conditions
- Kafka & Microservice Communication: Kafka transactions and idempotent consumers, Testing Kafka integration with base transactions, Implemented Saga pattern, Orchestration-based Saga with compensation transactions in microservices
## March, week III
### Fixes
- Subtask button now visible even when the subtask field is read only
- Fixed issue with Multi subform using cascade and external data causing application crash
- Fixed ticket form issue with detecting when the form finishes loading
- Fixed issue with adding a new property on ticket when properties were null; also ensured setting to NULL when last key is deleted from the map, preventing {} from remaining
- CSS fixes and action testing (First Entry and Validation) on “Paketi naloga” page in bankOcr project
### Improvements
- Updated Quarkus and other dependencies across listed projects
- Picker for tickets now allows filtering by project
- Added missing negation for "Editability" in required filters
- Ongoing work on COMPARE_FORM_ITEM filter, unified logic for visibility, editability, and required filters into a single component for consistency
- “My Team” query added to Homepage via MoProcess image
- Subtask button converted to link format (like Related Tickets)
- Support for nested subforms within multi-subform structure when using cascade and external data flag
- Finalized and deployed support for nested subforms in production
- AdvancedTable component: action column is now pinned to the right and doesn't require scrolling
- Updated Quarkus dependencies in MoCat, MoCentral, and MoExecutor; deployed to production (remaining projects had build/auth issues)
### New Features
- COMPARE_FORM_ITEM and COMPARE_TWO_FORM_ITEMS filters added:
- First compares current form item with another in the same form. Second compares two unrelated fields within the form
- Action system for AdvancedTable component: allows opening a form from the Homepage via button click and mapping values from the clicked row into form’s initial values
- Dynamic links in application header via Look and Feel configuration:Each link supports URL, ext code, icon, option to open in new tab, and tooltip. Absolute paths cause full reload; relative paths use Vue router. Tooltips support plain text or dynamic translation. Drag and drop enabled for custom sorting. 
## March, week II
### Fixes
- AdvancedTable- Fixed issues related to different source display permutations (edit mode, locked mode)
- Cascade- Resolved bug with the read only variant
- File Upload- Fixed issue preventing multiple files from being uploaded at once
- Featured Document- Featured document is now removed from results page when there are no results
- Search Quotes Handling- Quotes in search queries are now replaced with spaces
- File Deletion Control- The delete button in the file preview section is now hidden if it is not visible in the listing above
- Component Administration- Fixed issue with incorrect value saving when changing component type
- Ticket Loading Query- Restored ticket loading query on the Board page
### Improvements
- App Export/Import- Added app_map records to the export list along with NRNs for endpoint_smtp
- Ticket Redirection- Added a button in the ticket selection component that opens the selected ticket in a new window. Button is only visible when a ticket is selected
- AdvancedTable- Added single-choice mode for data_type=data and data_type=data_def (process file)
- Search Criteria- The doc_keywords field is now included in search criteria
- Search Ranking- doc_keywords and doc_kratakopis fields now contribute to search result ranking
- Metadata Links- Document metadata now contains a link to its corresponding ticket
- Homepage/Ticket List- Released optimized queries for "My Approvals" and "My Requests"
- Library Updates- Updated Quarkus and other dependencies across listed projects
- Ticket Picker- Added project selection as a filter option in the configuration
- Required Filter (Negation)- Negation feature was already implemented but was missing in Editability; added it there as well
- Compare Form Item Filter- Refactored underlying components so that Visibility, Editability, and Requirement filters share the same implementation, ensuring future updates apply to all three
- Quarkus Update on Projects- Updated dependencies on 3/5 targeted projects (MoCat, MoCentral, MoExecutor)
- UI Adjustments-Added padding below content. Replaced close icon on the banner close button
### New Features
- New Component - BannerNotification- Implemented with modal and notification modes. Demonstrated behavior with left-side menu and top positioning
- XML to JSON Conversion- Converted XML files to JSON format for imports of legacy systems data
- JSON Generation & SQL Script- Generated JSON for xml imports and an SQL script for NPL documents
## March, week I
### Fixes
- Completed fixes for maintaining mappings in project settings, including selecting existing references and directly creating new ones
- Fixed a bug in subform validation for fields with visibility and required properties
- Fixed a bug that allowed users to transition a ticket to the next state before the ticket finished loading
- AdvancedTable - Fixed bugs related to different permutations of source display (edit mode, locked mode)
- Cascade - Resolved an issue with the read only variant
- File Uploads - Fixed a problem with multiple file uploads where uploading more than one file simultaneously wasn't possible
### Improvements
- Knowledge Base - Fields like is_remote and url from process document records are now automatically indexed
- AdvancedTable - Added a single-choice mode for data_type=data and data_type=data_def (process file)
- Application Mapping - Connected the UI with util actions. CRUD operations now work properly. Added search and active-only filters to all queries listing application-related data. Added search and active-only filters to all queries listing application-related data
- BankOcrFrontend - Added logOperationModal to the "Packages of Orders" page. in the TransferOrder component, created the focusAfterLoadImage method and fixed the focus on the continueOrderButton. In the CheckCheck component, fixed resetting the serialNumberDisableModValidation parameter
- MoCentral - New "Banner" page was created on the "Settings" page, and a toasted component display was added to the BaseLayout component
- Created a modal mode on the BaseLayout component. Added a button in the form details that opens a modal for creating a component and adds the created component to the bottom of the currently open form
- In the processStateTransitionModal, created a link next to the "Form" field that opens the edit page for the selected form in a new tab
### New Features 
- Created a workflow for creating app map records, using an example with the SMTP endpoint in projects, along with util functions
- Created a new BannerNotification component for modal mode and standalone notification mode
## February, week IV
### Fixes
- SegmentedControl/ToggleButtons - Fixed issue with component rendering on the screen
- Form dropdown - Fixed lookup for files (ticket ID was not sent), fixed file name formatting
- User list with a dynamic source - Fixed issue with the filter operation
- Bug fix for Style overflow from ticket description to the entire portal
- BankOcrFrontend - fixed the init method for the TransferOrder
- bankOcrFrontend - fixed init method in the TransferOder component 
### Improvements
- Enhancement of Radio/ MultiCheckbox/ SegmentedControl/ ToggleButtons functionality - Support for filters in the mentioned component types implemented, related to the custom table
- Form dropdown functionality - Support for using source from the form included, besides the source from the properties map, in the dropdown list component where elements are from a subform
- Form administration functionality - Added component search in the form at the top of the page
- User list with a dynamic source functionality - "Filter loading mode" implemented
- User list with a dynamic source functionality - "Set value" functionality enabled
### New Features 
- Default Home Page - Mechanism for changing the default home page on the portal implemented. The setting is located on the Appearance page in Settings. It's possible to choose default, appdashboard and Home (servicehomepage)
- Form datepicker - Added configuration parameters to limit date selection. Parameter is relative. Time units (weeks, days, hours, minutes) are entered. Negative values can also be entered.The minimum relative value will block all dates before the calculated time.The maximum relative value will block all dates after the calculated time
- New SQL scripts for checking internal documentation
- BankOcr - created the onLoadImage method to display the spinner on order and reset urgentUi to false if there is no transactionType or it is empty on each loading of the transferOrder
## February, week III
### Fixes
- Parent ticket overview now correctly displayed on subticket
- Linked tickets:disabled auto conversion from Cyrillic to Latin characters
- Subform components: fixed default date value settings
### Improvements
- Ranking of filtered "the most" content based on matching search item and document headline
- Form item filters now support system fields ext_code, name, and description
- Under the hood improvement of datepicker and duration data types. Also added support for negative time values
### New Features 
- New file manager process permission and UI with support for multi-select
- New file manager functionality with the option for users with correct permissions to revert files from deleted
- User data configuration handling with client and server validation
- Added today and tomorrow as default date options
## February, week II
### **Fixes**
- Default value for date type now implemented correctly
- Translations imports now support inserting specific labels without need for corresponding system labels
- Fixed AppDashboard initial loading of datepicker for charts
- Fixed code for default date on forms
### **Improvements**
- AppDashboard report date picker 
- Linked tickets: added link to the ticket next to the connection
- Added link in accordance with permission schema
- Knowledge base "the most" content ("the most evaluated", "the most viewed", "the most liked") now supports filters
### **New Features** 
- Bulk edit enabled
## February, week I
### **Fixes**
- Fixed dynamic resizing in AppDashboard 
- Fixed filter in Reports column
- Fixed files and actions manipulation in AppDashboard
- Now policies are correctly applying on tickets created from other tickets.
### **Improvements**
- Dropdown lists now support user defined API and formatting
- RichTextEditor controls are now hidden if not in use/focus
- Improved subform for creating ticket from another ticket
### **New Features** 
- Under the hood features - New proxy related actions created, new jsonquery queries added
- **Office365 conectivity and email integration supported in latest release**
## January, week IV
### **Fixes**
- Fixed ticket export to Excel. 
- Fixed default filter read from project during change of current project using upper left cosco
- Homepage/My assignments corrected issue with search option which no longer opens ticket details
- Under the hood fixes of reports. Fixed an issue with reading data from tables with custom key columns
### **Improvements**
- Export to XML now read contacts data from parameters for better accuracy
- Next ticket row - button for adding new ticket is not longer enabled by default. It can be enabled from misc section of a project
- Under the hood improvements - removed URL logging on redirection API
### **New Features** 
- Created method for XML digital signature
- Created new action on mono process: export from custom table to Excel and sending to s3 bucket
- Added export to Excel action from custom tables (export_excel_from_custom_table)
- Now new tickets can be added from Documents page
## January, week III
### **Fixes**
- Knowledge base favourite document: removed double heart symbol
### **Improvements**
- Menu cleanup: Jira reports removed
- User permissions migrated and label changed
- Knowledge base style improved
- Reporter actions: enabled action initiation from ticket Reporter field
- Knowledge base UI: improved remote document display with larger popup and rearranged controls.  
### **New Features**
- Default portal language settings enabled in look&feel
- Added configuration option for text color and active window background color
- Enabled creation of custom remote tables and remote sql queries 
## January, week II
### **Fixes**
 - User policies: Fixed an issue with user policy rights selection
 - User policies: Fixed an issue with remote table filtering
 - Subtask files: Corrected file transfer from task to subtask
 - Mo Knowledge project: fixed URL encoding and XML parsing
### **Improvements**
 - Improved top menu navigation
 - KB remote document display: rearranged UI elements of remote document
