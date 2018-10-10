# Depreciated Commands & Features

## Depreciated from WinBuilder 082

These Winbuilder commands have not been implemented in PEBakery.

### DirCopy `[SHOW]`

When the `SHOW` flag was supplied with the `DirCopy` command Winbuilder would show the operating system's file copy progress dialog.

### DirDelete `[FAST]`

When this parameter was used, WinBuilder would rename the directory to a random name, and then execute the delete process in the background. PEBakery has a more reliable implementation of `DirDelete` making this flag unnecessary.

### ExtractAllFilesIfNotExist

No longer used. Can be accomplished with other commands.

### FileByteExtract

This command was originally designed for extracting resources from executable files and is no longer used. Resource extraction can be accomplished more effectively with other tools (eg. Resource Hacker).

### Hive,Delete/Load/Read/UnLoad/Write

These commands are no longer used in Winbuilder and have been replaced by RegHiveLoad/RegRead/RegWrite/etc.

### If,License

No longer used. Originally this command would display a dialog containing a license agreement and force the user to accept or reject the license. Because this required user interaction during the build it was rarely used because it slowed down the build process.

### If,Runs

This command would perform an user defined action if a specified executable was found to be running. It has not been used in any active projects.

### RegGetNext

This command was introduced in Winbuilder 071/072 in order to provide a way to enumerate driver classes in the registry. It has not been used an any active projects.

### RegReadBin / RegWriteBin

This command was a hack to allow writing unchecked values to the registry via a binary format because Delphi 7 doesn't support Unicode or 64bit QWORDS. It never did work correctly in Winbuilder and is no longer required as PEBakery has native support for QWORDs and Unicode strings in RegRead and RegWrite.

### Run [OUT:]

Winbuilder's implementation of the `Run` command allows for passing a parameter _by reference_ using the `OUT:<var>` directive. At the time of this writing there are no known projects using this functionality so implementation has been deferred. If you feel you need this functionality please open a support ticket.

### StrFormat,CharToOEM / OEMToChar

These functions were used to convert between the ANSI charset and the DOS charset, and were useful when dealing with special characters like "umlauts" and other similar markings. DOS charset is no longer used or supported in modern operating systems.

### System,Comp80

This command was used to force Winbuilder into compatibility mode with previous version when internal changes were made to the way variables were handled. PEBakery is modern implementation of the WinBuilder 082 feature set, older versions are not supported.

### System,FileRedirect / System,RegRedirect

PEBakery uses the .NET framework and will run in either x86 or x64 (AnyCPU), therefore WOW64 redirection is unnecessary.

### System,IsTerminal

Was used in older projects to detect if Winbuilder was running in a terminal server session. This was problematic because of the way older versions of Terminal server handled writing certain configuration files. No longer used by any active projects and should not be necessary with modern versions of Windows.

### System,Log

This command was originally was intended to allow a developer to disable logging of API/Macro commands in order to keep the build log from inflating. PEBakery has options that allow the user to toggle logging of Macro commands making this command unnecessary.

### System,SplitParameters

Following Winbuilder's default behavior PEBakery will always split parameters.

### TXTAddLine - **PLACE**

WinBuilder's implementation of `TxtAddLine` allowed for an `Action` called **Place** which would allow the developer to specify a line number where the text should be inserted. This feature was depreciated in PEBakery due to lack of perceived usefulness.

### WebGet `[MD5]` `[Comment]` `[Timeout]`

Winbuilder's Webget implementation had multiple issues and was completely rewritten for PEBakery. The MD5/Command/Timeout flags were depreciated and modern hash verification commands implemented.

## Commands that will be depreciated

These commands are fully functional within PEBakery but will be removed in a future release. Some commands are disabled by default but can be enabled by a compatibility option. It is advised to avoid using these commands in your projects and replace them as soon as possible.

### GetParam / PackParam

These commands were added to Winbuilder in an attempt to work around the limit of 9 parameters that could be passed to a Run/Exec command.

The intention was that multiple parameters could be "packed" into an array/list and passed as a single parameter to the called _section_ where they could be expanded back to their original variables, however the command is totally broken in Winbuilder 082 so projects never made use of the functionality.

PEBakery supports an infinite number of section parameters, as well as list structures via the `List` command so Get/Pack Param are no longer necessary.

### Legacy Branch Conditions

Legacy branch conditions such as `NOTEXISTFILE` and `NOTEXISTDIR` are depreciated in favor of using the `Not` operator (eg. `If,Not,EXISTDIR`...). This is the recommended syntax in Winbuilder so legacy branch conditions are disabled by default in PEBakery. They can be enabled with a compatibility option.

### Loop - `<Letter>`

WinBuilder's `Loop` implementation allows incrementing alphabetically as well as numerically. This behavior is disabled in PEBakery but can be enabled with a compatibility option. PEbakery supports alphabetically looping with the `LoopLetter` command.

### Set,`<%interfaceControl%>`

Winbuilder allows the `Set` command to modify interface control values, however usage is inconsistent with other behavior of the `Set` command. PEBakery depreciated this behavior in favor of the more flexible `WriteInterface` command. Winbuilder's `Set` behavior can be toggled with a compatibility option.

### StrFormat,Div

Replaced by `Math,Div`

### StrFormat,ShortPath / LongPath

Success of conversion to short path depends on registry value `HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation`, thus this command cannot be guaranteed to work properly in every system.

### StrFormat,Mult

Replaced by `Math,Mul`

### System,HasUAC

Currently PEBakery always returns `True` to this command.

User Account Control (UAC) is enabled by default in all supported versions of Windows making this command largely unnecessary. Furthermore many users are not aware of the dangers of disabling UAC, therefore it is better to design your project to work on UAC enabled systems rather then encourage users to disable security features in order to build a project.

### System,RebuildVars

This command is obsolete in Winbuilder 082 as was originally implemented in version 075/076 for compatibility reasons replacing `System,RefreshVars` after engine improvements made the command largely unnecessary. Prior to Winbuilder 075 variables defined in the `[Variables]` section required a manual Refresh/Rebuild once they were dynamically modified with the `Set` command. For further reading check out [this post](http://reboot.pro/topic/4663-variables/).

Currently PEBakery resets variables to the original value as it was defined in the `[Variables]` section.

### WebGetIfNotExist

This command is broken in Winbuilder 082, and it was thought it would be better to implement this as a macro.

### Visible

Winbuilder's `Visible,<control>,PERMENENT` command will be depreciated in favor of PEBakery's `WriteInterface,Visible` command.

## Depreciated Constant/Fixed Variables

Winbuilder presets a number of constant/fixed variables. Most of these variables contain information that can be easily obtain through other means and some don't have any use at all. The PEBakery team believes that the project/script author should be the one to decide what variables they want defined and what they should be named, not PEBakery. For this reason PEBakery limits itself to defining essential variables such as `%BaseDir%, %ProjectDir%, %ScriptFile%` and leaves the decision to define additional variables up to the project/script author to implement as they see fit.

The following variables have been depreciated. A small subset of environment variables can be enabled using the compatibility option _Enable Environment Variables_ however it is strongly advised to use alternative methods.

| Variable | Description | PEBakery Alternative |
| --- | --- | --- |
| %FileVersion% | Winbuilder returned the file version of Winbuilder.exe | PEBakery provides this information via the `%PEBakeryVersion%` variable.
| %WBExe% |  The path to Winbuilder.exe | This is PEBakery, not Winbuilder. |
| %WBLanguage% | Winbuilder Language | This is PEBakery, not Winbuilder. |
| %AppMode% | Winbuilder returns `wbaNormal` if the program is started normally. | This is PEBakery, not Winbuilder. |
| %RegDataType% | Winbuilder sets this variable to the data type of the registry value accessed via the most recent `RegRead` command. | Not used in any projects. No valid use cases in active projects. |
| %Tools% | Winbuilder sets this to `%BaseDir%\Projects\Tools` | You can set this to whatever you want. |
| %Day% | Winbuilder returned the current weekday. | Use `StrFormat,Date,%Day%,"d"` |
| %Year% | Winbuilder returned the current year. | Use `StrFormat,Date,%Year%,"yyyy"` |
| %Month% | Winbuilder returned the current month. | Use `StrFormat,Date,%Month%,"m"` |
| %TempDir% | Windows Temp Directory | Use `System,GetENV,"TEMP",%TempDir%` |
| %ProgramFilesDir% | Windows Program Files Directory | Use `System,GetENV,"ProgramFiles",%ProgramFilesDir%` |
| %WindowsDir% | Windows Directory | Use `System,GetENV,"windir",%WindowsDir%` |
| %UserName% | The name of the current user. | Use `System,GetENV,"USERNAME",%UserName%` |
| %UserProfile% | The current user's home directory. | Use `System,GetENV,"USERPROFILE",%UserProfile%` |
| %ProcessorType% | Winbuilder returns the operating system architecture as defined by SYSTEM_INFO. | Use `System,GetENV,"PROCESSOR_ARCHITECTURE",%ProcessorType%` |
| %HostOS% | Winbuilder returns a string representing the current OS (Ex. Win7). Returns an empty string in recent versions of Windows. | Consider checking the Windows version/build number instead. |
| %Wow64% | Winbuilder returns `True` if it is running under a 64bit operating system. | Modern operating systems are all 64bit. If you still need to test this condition consider useing `System,GetENV,"PROCESSOR_ARCHITECTURE",%ProcessorType%` |
| %Wow64Dir% | Winbuilder returns the path of the WindowsOnWindows64 subsystem. Typically `C:\Windows\SysWOW64` | Use `System,GenENV,"windir",%WindowsDir%    Set,%Wow64Dir%,"%WindowsDir%\SysWOW64` |
| %Programs64% | Winbuilder returns the path where 64bit Program Files are stored. | Use `System,GetENV,"ProgramFiles",%ProgramFilesDir%` |