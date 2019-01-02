# System,LoadNewScript

Refresh a specific script or path in the project.

Wildcards (* ?) are supported and can be used to load multiple scripts at one time.

## Syntax

```pebakery
System,LoadNewScript,<FilePath>,<TreePath>[,PRESERVE][,NOWARN][,NOREC]
```

### Arguments

| Argument | Description |
| --- | --- |
| FilePath | The path to an **new** script file or path to load. Wildcards (* ?) are supported. |
| TreePath | The location in the project tree where the script(s) will be loaded. This path should not include the projects root node. |

### Flags

The following flags can be used independently and can be specified in any order.

| Flag | Description |
| --- | --- |
| NOREC | **(Optional)** Do not recurse subdirectories. When using wildcards all directories under `FilePath` will be scanned. Use this flag to disable this behavior. |
| NOWARN | **(Optional)** When the `PRESERVE` flag is specified attempting to load a script that is already present in the project tree will result cause the operation to fail. Use the `NOWARN` flag to ignore the error and continue processing. |
| PRESERVE | **(Optional)** Do not load scripts that already exist in the project tree. |

## Remarks

This command can be used to load a specific script or path into the project tree and performs similar to the `System,RefreshAllScripts` command with the exception that only the specified file(s) are refreshed. This can save time if you don't need to refresh the entire project tree, which could span multiple projects and dozens of scripts.

This command is intended for loading **new** scripts into the project tree. If you need to refresh and existing script use the `RefreshScript` command instead.

Due to a system limitation PEBakery cannot load scripts from another project into the current project.

When using wildcards all directories under `FilePath` are scanned for the specified pattern. Use the `NOREC` flag to disable this behavior. 

## Related

[System,RefreshAllScripts.md](./RefreshAllScripts.md), [System,RefreshScript.md](./RefreshScript.md)

## Examples

### Example 1

```pebakery
[Main]
Title=LoadNewScript Example
Author=Homes32
Description=Demonstrate usage of the System,LoadNewScript command.
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
System,LoadNewScript,%myScript%,Extra

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