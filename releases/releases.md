# NeoBee Releases 2025
## March, week III
### Fixes
- Subtask button now visible even when the subtask field is read only
- [BUG] [frontend] [form] Fixed issue with Multi subform using cascade and external data causing application crash
- [BUG] Fixed ticket form issue with detecting when the form finishes loading
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
- BankOCR Project - Fixed validation for the "reference number" field in TransferOrder and CheckOrder components. Fixed a bug in the checkSrbGovermentReferenceNumber method within the TransferOrder and CheckOrder components
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
- BankOcr - jQuery version upgraded due to a security test issue with the client
- Form dropdown functionality - Support for using source from the form included, besides the source from the properties map, in the dropdown list component where elements are from a subform
- Form administration functionality - Added component search in the form at the top of the page
- User list with a dynamic source functionality - "Filter loading mode" implemented
- User list with a dynamic source functionality - "Set value" functionality enabled
### New Features 
- Default Home Page - Mechanism for changing the default home page on the portal implemented. The setting is located on the Appearance page in Settings. It's possible to choose default, appdashboard and Home (servicehomepage)
- Form datepicker - Added configuration parameters to limit date selection. Parameter is relative. Time units (weeks, days, hours, minutes) are entered. Negative values can also be entered.The minimum relative value will block all dates before the calculated time.The maximum relative value will block all dates after the calculated time
- New SQL scripts for checking internal documentation for NIS and it's subsidaries
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
- NisKB: "the most" content ("the most evaluated", "the most viewed", "the most liked") now supports filters
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
 - NisKB remote document display: rearranged UI elements of remote document
