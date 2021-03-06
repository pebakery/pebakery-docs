# PEBakery Logs

The PEBakery log viewer allows you to view and export various logs generated by PEBakery.

Logs are stored in a SQLLite database *(%BaseDir%\Database\PEBakeryLog.db)*. Additional options are available in PEBakery's settings that allow you to control different aspects of event logging.

## Log Types

PEBakery generates several different log types. Each type is outlined below.

### System Log

The `System Log` tab contains events related to PEBakery's operation.

Events found in this log include:
 
 - Script & Project loading
 - Build, Codebox, and Run start/stop
 - Cache operations
 - Script interface rendering errors
 
### Build Logs

The `Build Log` tab contains logs from each build, including codebox, individual script runs, and interface control events.

#### Select Build

Select the log for the build you wish to view from this dropdown.

#### Select Script

Select an individual script log or view the overall build summary.

#### Statistics Tab

Displays statistics, including the number of errors and warnings produced by the build.

#### Simple Logs Tab

Display a plain text version of the currently selected log.

#### Full Logs Tab

Displays the full detailed log of the currently selected log. Information is broken out into a table with various columns containing information about the event. You may show or hide individual columns using the context menu or by clicking the `Options` button.

| Column Name | Description |
| --- | ---|
| Time | Time-stamp when the event occurred. |
| Depth | Position in the processing tree. Each branch condition (Run, Exec, Loop, etc.) increases the depth. |
| State | Error State - Valid states include:
|| Error - Critical events that cause a script or build to fail. |
|| Ignore - Events that may have been triggered by a Warning or Error but were suppressed by the script. (eg. `NOWARN` flag) |
|| Info - Informational events such as comments and `Echo` commands. |
|| Overwrite - An existing file or registry value has been overwritten. |
|| Success - The command executed successfully. | 
|| Warning - Non-Fatal errors or events that may require attention. |
| Flags | Special indicators |
|| C - Comment |
|| M - Macro Command |
|| R - Referenced Script (ie. A script called from another script via `Run` or `Exec`). |
|| E - Exceptions - Errors and Stack Traces generated by the PEBakery Engine. |
| Message | The result of the command. |
| Raw Code | The original statement that was executed. |
| Line Number | The line number of the executed statement. |
| Script Origin | If the executed code resides in a script other then the currently processing script this column will contain the name of the referenced script. |

#### Variables Tab

Contains a list of all defined variables and their value as of the time the script execution was terminated.

## Clearing Logs

Over time your log database can grow to be quite large. In order to reclaim disk space You may use the `Clear Log` button on the log window or the `Clear Logs` button located in **PEBakery > Settings > Logs**.

## Exporting Logs

Logs may be exported in Text or HTML format.

### Text Logs

Text logs are formatted as UTF-8 BOM text files and follow the `Simple Log` layout. Text logs are ideal because of their small size and their compatibility with a wide variety of editors and search tools.

### HTML Logs

HTML formatted logs follow the `Full Log` layout and are designed for troubleshooting and easy navigation.