# Compatibility Settings

Compatibility options are designed to emulate various WinBuilder bugs and quirks. Settings are configured independently for each project, allowing multiple projects to exist in the same `%BaseDir%\Projects` folder without being affected by conflicting settings.

Whenever possible PEBakery development attempts to keep backward compatibility with existing WinBuilder 082 commands, however in order to fix serious Winbuilder bugs, improve syntax, and promote consistency across commands, breaking changes cannot always be avoided. In the event a script breaking change is made to an existing Winbuilder era command PEBakery provides compatibility options that enable the engine to revert to the previous behavior. This allows developers the opportunity to update their projects/scripts without suffering downtime.

## Settings

Compatibility settings may be configured via the **PEBakery > Settings > Compat** tab or by manually editing `PEBakeryCompat.ini` in the project's root directory *(eg. C:\PEBakery\Projects\Win10PE\PEBakeryCompat.ini)*.

### Asterisk Bug

| Setting | Ini Key | Description |
| --- | --- | --- |
| Simulate WinBuilder's *.* bug in DirCopy | AsteriskBugDirCopy | When using wildcards to copy subdirectories, files that exist at the same level are copied as well. |
| Simulate WinBuilder's *.* bug in folder.project | AsteriskBugDirLink | When using wildcards to find folder links, scripts in the root of the specified folder are ignored and only scripts in sub-folders are loaded. |

### Command

| Setting | Ini Key | Description |
| --- | --- | --- |
| FileRename and DirMove work like PathMove | FileRenameCanMoveDir | Allows `FileRename` and `DirMove` command to move files. |
| Allow letter in Loop | AllowLetterInLoop | Allows the Loop command to increment alphabetically as well as numerically.|
| Enable deprecated legacy branch conditions | LegacyBranchCondition | Allow legacy conditions such as `NOTEXISTFILE`, `NOTEXISTDIR`, etc. (Replaced by `If,Not,ExistFile`)|
| Allow variables in RegWrite's `<HKey>`, `<ValueType>` argument | LegacyRegWrite | Allows variables to be used as arguments in RegWrite. |
| Allow Set to modify interface controls | AllowSetModifyInterface | Allows the `Set` command to write values to interface controls. (eg. Textlabel value). (Replaced by `WriteInterface,Value...`) |
| Enable legacy interface commands (eg. Visible) | LegacyInterfaceCommand | Enable legacy commands such as `Visible`. (Replaced by `WriteInterface,Visible...`)|
| Enable legacy section parameter commands e.g. PackParam) | LegacySectionParamCommand | Allows you to use the deprecated `PackParam` command. |

### Script Interface

| Setting |Ini Key | Description |
| --- | --- | --- |
| Ignore width of WebLabel | IgnoreWidthOfWebLabel | WinBuilder ignores the specified width of WebLabel controls and sizes them to fit the text. Use this option to replicate this behavior. |

### Variable

| Setting | Ini Key | Description |
| --- | --- | --- |
| Overridable fixed variables | OverridableFixedVariables | Allow constant/fixed variables to be overwritten. |
| Overridable loop counter (#c) | OverridableLoopCounter | Winbuilder allows overwriting of the loop counter `#c` during a loop, but then resets the value on the next iteration. Some poorly written scripts use this token as a 'disposable' variable. |
| Enable environment variables | EnableEnvironmentVariables | Enable a limited set of pre-define environment variables. |
| Disable extended section parameters (e.g. #a, #r) | DisableExtendedSectionParams | Disables the `#a` and `#r` tokens. This may be desirable if you use statements such as `TxtAddline,%w%,"#RequireAdmin",Append` where PEBakery can mistake `#R`  for the `#r` token. |

## Examples

The following example shows `PEBakeryCompat.ini` with all compatibility options enabled for the `Win10PE` project.

Path: `C:\PEBakery\Projects\Win10PE\PEBakeryCompat.ini`

```ini
[PEBakeryCompat]
AsteriskBugDirCopy=True
AsteriskBugDirLink=True
FileRenameCanMoveDir=True
AllowLetterInLoop=True
LegacyBranchCondition=True
LegacyRegWrite=True
AllowSetModifyInterface=True
LegacyInterfaceCommand=True
LegacySectionParamCommand=True
IgnoreWidthOfWebLabel=True
OverridableFixedVariables=True
OverridableLoopCounter=True
EnableEnvironmentVariables=True
DisableExtendedSectionParams=True
```
