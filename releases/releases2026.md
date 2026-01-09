# NeoBee Releases 2026
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
