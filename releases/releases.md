# NeoBee Releases 2025
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
