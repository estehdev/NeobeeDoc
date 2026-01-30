# NeoBee Releases 2026
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
