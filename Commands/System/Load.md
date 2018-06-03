# System,Load

Scans the specified path for new/modified projects and scripts and adds them to the project tree.

## Syntax

```pebakery
System,Load,<FilePath>,[NOREC]
```

### Arguments

| Argument | Description |
| --- | --- |
| FilePath | The path to the script file to load. Wildcards (* ?) are supported and can be used to scan multiple files. |

### Flags

| Flag | Description |
| --- | --- |
| NOREC | **(Optional)** Do not recurse subdirectories. - When using wildcards all directories under `FilePath` are scanned. Use this flag to disable this behavior. |

## Remarks

This command can be used to rebuild the project tree when a script is added or modified and performs similar to the  `System,LoadAll` command with the exception that only the specified file(s) are loaded. This can save time if you don't need to refresh the entire project tree, which could span multiple projects and dozens of scripts.

Due to a system limitation PEBakery cannot `Load` the current script `%ScriptFile%` during a project build. The command will take affect after the current build finishes.

## Related

[System,LoadAll](./LoadAll.md)

## Examples

### Example 1

```pebakery
[Main]
Title=Load Example
Author=Homes32
Description=Demonstrate usage of the System,Load command.
Version=1
Level=5

[Interface]
CB_Recurse="Scan inside subdirectories",1,3,15,30,200,20,True
BTN_Load=Load,1,8,15,60,80,25,Process,0,False,_Process_,False
BTN_Clean=Cleanup,1,8,100,60,80,25,Clean,0,True,_Clean_,True

[variables]
%myProject%=%BaseDir%\Projects\myProject\script.project
%myScript%=%BaseDir%\Projects\myProject\myScript.script
%mySubDir%=%BaseDir%\Projects\myProject\SubDir\folder.project
%myScript2%=%BaseDir%\Projects\myProject\SubDir\myScript2.script

[Clean]
Echo,"Removing myProject Example..."
If,EXISTDIR,%BaseDir%\Projects\myProject\,DirDelete,%BaseDir%\Projects\myProject\
System,LoadAll

[process]

If,Not,ExistFile,%myProject%,FileCreateBlank,%myProject%
If,Not,ExistFile,%myScript%,FileCreateBlank,%myScript%

// Project
IniWrite,%myProject%,Main,Title,myProject
IniWrite,%myProject%,Main,Author,Homes32
IniWrite,%myProject%,Main,Description,"A brand new project!"
IniWrite,%myProject%,Main,Version,1
IniWrite,%myProject%,Main,Level,5

TXTAddLine,%myProject%,"[Variables]",Append
TXTAddLine,%myProject%,"",Append
TXTAddLine,%myProject%,"[Process]",Append
TXTAddLine,%myProject%,"[Interface]",Append
TXTAddLine,%myProject%,"",Append

// Script
IniWrite,%myScript%,Main,Title,myScript
IniWrite,%myScript%,Main,Author,Homes32
IniWrite,%myScript%,Main,Description,"A brand new Script!"
IniWrite,%myScript%,Main,Version,1
IniWrite,%myScript%,Main,Level,5
IniWrite,%myScript%,Main,Selected,False

TXTAddLine,%myScript%,"[Variables]",Append
TXTAddLine,%myScript%,"",Append
TXTAddLine,%myScript%,"[Process]",Append
TXTAddLine,%myScript%,"[Interface]",Append
TXTAddLine,%myScript%,"",Append

// Script subdir
//IniWrite,%mySubDir%,Main,Title,myApps
//IniWrite,%mySubDir%,Main,Author,Homes32
//IniWrite,%mySubDir%,Main,Description,"A folder for myApps"
//IniWrite,%mySubDir%,Main,Version,1

// Script in subdir
IniWrite,%myScript2%,Main,Title,myScript2
IniWrite,%myScript2%,Main,Author,Homes32
IniWrite,%myScript2%,Main,Description,"A brand new Script in a subdir!"
IniWrite,%myScript2%,Main,Version,1
IniWrite,%myScript2%,Main,Level,5
IniWrite,%myScript2%,Main,Selected,False

TXTAddLine,%myScript2%,"[Variables]",Append
TXTAddLine,%myScript2%,"",Append
TXTAddLine,%myScript2%,"[Process]",Append
TXTAddLine,%myScript2%,"[Interface]",Append
TXTAddLine,%myScript2%,"",Append

// Now we need to call the following command to get our new project and script to show up in the main window.
If,%CB_Recurse%,Equal,True,Begin
  // Scan the following directories and all subdirectories.
  Echo,"Loading all Scripts under %BaseDir%\Projects\myProject\"
  System,Load,%BaseDir%\Projects\myProject\*.*
End
Else,Begin
  // Do not scan subdirectories
  Echo,"Loading only scripts located in the %BaseDir%\Projects\myProject\ directory."
  System,Load,%BaseDir%\Projects\myProject\*.*,NOREC
End
```