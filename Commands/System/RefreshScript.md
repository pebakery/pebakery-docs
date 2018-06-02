# System,RefreshScript

Refresh a specific script or path in the project.

Wildcards (* ?) are supported and can be used to refresh multiple scripts at one time.

## Syntax

```pebakery
System,RefreshScript,<FilePath>[,NOREC]
```

### Arguments

| Argument | Description |
| --- | --- |
| FilePath | The path to an **existing** script file to refresh. Wildcards (* ?) are supported. |

### Flags

| Flag | Description |
| --- | --- |
| NOREC | **(Optional)** Do not recurse subdirectories. |

## Remarks

This command can be used to refresh a specific script the project tree and performs similar to the `System,RefreshAllScripts` command with the exception that only the specified file(s) are refreshed. This can save time if you don't need to refresh the entire project tree, which could span multiple projects and dozens of scripts.

The specified script must currently exist in the project tree or the operation will fail. If you need to load a new script into the project use the `LoadNewScript` command instead.

Due to a system limitation PEBakery cannot Refresh the current script `%ScriptFile%` during a project build. The command will take affect after the current build finishes.

When using wildcards all directories under `FilePath` are scanned for the specified pattern. Use the `NOREC` flag to disable this behavior. 

## Related

[System,LoadNewScript.md](./LoadNewScript.md), [System,RefreshAllScripts.md](./RefreshAllScripts.md)

## Examples

### Example 1

```pebakery
[Main]
Title=RefreshScript Example
Author=Homes32
Description=Demonstrate usage of the System,RefreshScript command.
Version=1
Level=5

[Interface]
BTN_Load=Refresh,1,8,15,60,80,25,Process,0,False,_Process_,False
BTN_Clean=Cleanup,1,8,100,60,80,25,Clean,0,True,_Clean_,True

[variables]
%myScript%=%ProjectDir%\myScript.script

[Clean]
Echo,"Removing myScript Example..."
If,EXISTFILE,%myScript%,FileDelete,%myScript%
System,RefreshAllScripts

[process]
If,Not,ExistFile,%myScript%,FileCreateBlank,%myScript%

// Create a new Script
IniWrite,%myScript%,Main,Title,myScript
IniWrite,%myScript%,Main,Author,Homes32
IniWrite,%myScript%,Main,Description,"A brand new Script!"
IniWrite,%myScript%,Main,Version,1
IniWrite,%myScript%,Main,Level,5
IniWrite,%myScript%,Main,Selected,False

// load it into our project
System,LoadNewScript,%myScript%,%ProjectName%

// Make some modifications to our script
TXTAddLine,%myScript%,"[Variables]",Append
TXTAddLine,%myScript%,"",Append
TXTAddLine,%myScript%,"[Process]",Append
TXTAddLine,%myScript%,"[Interface]",Append
TXTAddLine,%myScript%,"",Append

// refresh our script so our modifications take effect
Echo,"Refreshing %myScript%..."
System,RefreshScript,%myScript%
```