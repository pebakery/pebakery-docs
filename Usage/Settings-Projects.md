# Project Settings

Settings related to the selected project.

## Settings

Project settings may be configured via the **PEBakery > Settings > Projects** tab or by manually editing `PEBakery.ini` located in PEBakery's root directory *(eg. C:\PEBakery\PEBakery.ini)*.

### Default Project

| Setting | Description |
| --- | --- |
| Default Project | Project | DefaultProject | Specifies the "Startup Project" that will be automatically selected when PEBakery is launched. |

### Source Setup (Legacy)

This section is included for backwards compatibility with Winbuilder and allows for configuration of variables associated with the source and output directory fields located on Winbuilder's `Source` tab.

Modern projects should disable these settings to avoid confusion.

| Setting | Description |
| --- | --- |
| Project to Configure | Select the project to configure sources for. |
| Source Directory | Sets the value of the `%SourceDir%` variable. |
| Target Directory | Sets the value of the `%TargetDir%` variable. |
| ISO File | Sets the value of the `%ISOFile%` variable. |