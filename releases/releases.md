#2025
# NeoBee Releases
## January, week II
### **Fixe **
 - User policies: Fixed an issue with user policy rights selection
 - User policies: Fixed an issue with remote table filtering
 - Subtask files: Corrected file transfer from task to subtask
 - Mo Knowledge project: fixed URL encoding and XML parsing
### **Improvements**
 - Improved top menu navigation
 - NisKB remote document display: rearranged UI elements of remote document

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

## January, week IV
### **Fixes**
- Corrected issue with font size change not applying correctly in menu
- Corrected representation of user group initial in user group labels
- Optimized display of files in tickets on smaller screens
- Crawler: Fixed URL code, added https:// for recording
### **New Features**
- Added URL copy button in look6feel. Logo URL redirect action in accordance with images in look&feel.
- Knowledge base search results from remote sources now showing link alongside result. Link can be opened in separate tab.
- UI: New actions for translations listing. Translation sources now can be exported to Excel
- UI: Added option for display and export of system labels
- Crawler: added new column for content hash in the table
- Crawler: created new table es_crawler, new actions create crawler, list crawler and list crawler by ID
- Crawler: added actions update and execute.

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
