# NeoBee Releases 2025
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
-AppDashboard – Fixed an issue with adding actions to components on the dashboard.
-Validation on Multi Subform – Fixed an issue where required fields inside multi-subform components failed validation when no values were present.
-User Settings local storage – Fixed incorrect loading of other users' settings from local storage.
### Improvements
-AppDashboard external Value - Added support for external values for multiple dropdown components.
-AppDashboard date filtering – Added support for filtering a table using date component values configured in an action.
-Barcode Text Positioning – Enabled positioning text around barcodes on all four sides, and added configuration for barcode size.
-Sortable Table UI – Sort arrows in tables are now positioned to the left of column headers.
-Reconciliation Deadline Display – If the individual deadline differs from the global approval deadline (approve_deadline_global), both values will now be shown.
### New Features
-AppDashboard – Fixed an issue with adding actions to components on the dashboard.
-Validation on Multi Subform – Fixed an issue where required fields inside multi-subform components failed validation when no values were present.
-User Settings local storage – Fixed incorrect loading of other users' settings from local storage.
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
