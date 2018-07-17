# Deprecated Commands

## Deprecated from WinBuilder 082

These Winbuilder commands are not implemented in PEBakery.

### Run - OUT:

Winbuilder's implementation of the `Run` command allows for passing a parameter _by reference_ using the `OUT:<var>` directive. At the time of this writing there are no known projects using this functionality so implementation has been deferred. If you feel you need this functionality please open a support ticket.

### FileByteExtract

No longer used. Can be accomplished with other tools.

### RegReadBin / RegWriteBin

Not needed. PEBakery has native support for QWORDs and Unicode strings in RegRead and RegWrite.

### ExtractAllFilesIfNotExist

No longer used. Can be accomplished via other methods.

### StrFormat,CharToOEM / OEMToChar

DOS charset is no longer used.

### System,Comp80

PEBakery is new implementation of WinBuilder 082, no room for WinBuilder 080.

### System,FileRedirect / RegRedirect

PEBakery can be compiled into AnyCPU / x64, it can run without WOW64.

### System,IsTerminal

No longer used.

### System,Log

No longer used.
This command was originally was intended to allow a developer to disable logging of API/Macro commands in order to keep the build log from inflating. PEBakery has a global option in Settings > Logging > `Log Macro` that allows the user to toggle logging of Macro commands.

### System,SplitParameters

No longer used, PEBakery will always split parameters.

### TXTAddLine - **PLACE**

WinBuilder's implementation of `TxtAddLine` allowed for an `Action` called **Place** which would allow the developer to specify a line number where the text should be inserted. This feature was depreciated in PEBakery due to lack of perceived usefulness.

### If,License

No longer used.

## Commands that will be deprecated

These commands are fully functional within PEBakery but will be removed in a future release. It is advised to avoid these commands in your projects.

### WebGetIfNotExist

This command is broken in WB082, and it is better to implement this as macro.

### StrFormat,ShortPath / LongPath

Success of conversion to short path depends on registry value `HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation`.

Thus this commands cannot be guaranteed to work properly in every system.

### System,HasUAC

Currently PEBakery always returns `True` to this command.

User Account Control (UAC) is enabled by default in all supported versions of Windows making this command largely unnecessary. Furthermore many users are not aware of the dangers of disabling UAC, therefore it is better to design your project to work on UAC enabled systems rather then encourage users to disable security features in order to build a project.

### System,RebuildVars

Different from its name implies, this command just clear variables in WB082.

Currently PEBakery reset variables to default script variables.

### GetParam / PackParam

Those commands are totally broken in WB082, so it was not used.

PEBakery supports infinite number of section parameter, so these commands are no longer necessary.
