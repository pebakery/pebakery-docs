# System,RefreshAllScripts

**Alias:** `System,RescanScripts`

Scans the *Projects* directory for new/modified projects and scripts and adds them to the project tree.

## Syntax

```pebakery
System,RefreshAllScripts
```

### Arguments

This command has no arguments.

## Remarks

This command can be used to rebuild the project tree when a script is added or modified and performs the same operation as pressing the **Refresh** button on the main window.

## Related

[System,Load](./Load.md)

## Examples

### Example 1

```pebakery
[Main]
Title=RefreshAllScripts Example
Author=Homes32
Description=Demonstrate usage of the System,RefreshAllScripts command.
Version=1
Level=5
Selected=True

[Interface]
BTN_Clean=Cleanup,1,8,100,60,80,25,Clean,0,True,_Clean_,True

[variables]
%myProject%=%BaseDir%\Projects\myProject\script.project
%myScript%=%BaseDir%\Projects\myProject\myScript.script

[Clean]
Echo,"Removing myProject Example..."
If,EXISTDIR,%BaseDir%\Projects\myProject\,DirDelete,%BaseDir%\Projects\myProject\
System,RefreshAllScripts

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

// Now we need to call the following command to get our new project and script to show up in the main window.
System,RefreshAllScripts
```