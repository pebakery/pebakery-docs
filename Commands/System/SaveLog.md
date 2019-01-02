# System,SaveLog

Exports the current logfile.

## Syntax

```pebakery
System,SaveLog,<DestPath>[,Format]
```

### Arguments

| Argument | Description |
| --- | --- |
| DestPath | The full path where the log will be saved. If the file exists it will be overwritten. |
| Format | Logs can be exported to the following formats: |
|| HTML - **(Default)** Exports the log as an html document that can be easily viewed in a web browser. |
|| Text - Exports the log as a machine readable UTF8 .txt file. |

## Remarks

None.

## Related

## Examples

### Example 1

Save the log in both Text and HTML format with the date and time in the filename.

```pebakery
[Main]
Title=SaveLog Example
Author=Homes32
Description=Demonstrate usage of the System,SaveLog command.
Version=1
Level=5

[Interface]

[variables]

[process]
Echo,"Doing some stuff...."
FileCreateBlank,%BaseDir%\Temp\myFile.txt
FileDelete,%BaseDir%\Temp\myFile.txt
// Get a timestamp for our log file name to avoid overwrites
StrFormat,DATE,%Timestamp%,"yyyy-mmm-dd-hhnn"
Echo,"Exporting Log as [HTML]..."
System,SaveLog,%BaseDir%\%Timestamp%-myLog.html
Echo,"Exporting Log as [Text]..."
System,SaveLog,%BaseDir%\%Timestamp%-myLog.txt,Text
Echo,"Done."
```

### Example 2

This example saves the build log, then compresses the log and several ancillary log files into an archive that can be easily transported for debugging.

```
[Main]
Title=SaveLog Example 2
Author=Homes32
Description=Demonstrate usage of the System,SaveLog command.
Version=1
Level=5

[Interface]

[variables]

[process]
Echo,"Archiving Support Log...."
FileCreateBlank,%BaseDir%\Temp\myLog.log
FileCreateBlank,%BaseDir%\Temp\anotherLog.txt
// Get a timestamp for our archive file name to avoid overwrites
StrFormat,DATE,%Timestamp%,"yyyy-mmm-dd-hhnn"
Echo,"Exporting Log as [HTML]..."
System,SaveLog,%BaseDir%\Temp\BuildLog.html
// Compress our build log and our other logs into a zip archive
Compress,Zip,%BaseDir%\Temp\myLog.log,%BaseDir%\%Timestamp%-%ProjectTitle%-Logs.zip
Compress,Zip,%BaseDir%\Temp\anotherLog.txt,%BaseDir%\%Timestamp%-%ProjectTitle%-Logs.zip
Compress,Zip,%BaseDir%\Temp\BuildLog.html,%BaseDir%\%Timestamp%-%ProjectTitle%-Logs.zip

Echo,"Done."
```