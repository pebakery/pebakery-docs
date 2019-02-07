# Variables

Variables are used to store a value in memory while a script is processing.

## Declaring Variables

Variables consist of a unique name used to identify the variable and must be enclosed in percent signs `%`. Variable names are case insensitive, so `%myVar%` is the same as `%MYVAR%`.

Variables can be defined in several different ways:

Predefined variables defined in the script's [Variables] section

```pebakery
[Variables]
%myVar%="Hello World!"
```

Dynamically at runtime using the `Set` and `AddVariables` commands

```pebakery
Set,%myVar%,12345
AddVariables,%ScriptFile%,AlternativeVariables
```

As a return value of a command such as `StrFormat`, `Math`, or `RegRead`.

```pebakery
StrFormat,Left,"Hello World!",5,%result%
```

## Variables Search Order

It is possible that local variable may share the same name with a project global variable. In the event a name collision occurs the following order will be used to determine the value to be use within the script.

### PEBakery standard

1. Fixed Variables
1. Local Variables
1. Global Variables

### WinBuilder Compatible

When the compatibility option `Overridable Fixed Variables` is enabled the following search order is used.

1. Local Variables
1. Global Variables
1. Fixed Variables

## Variable Types

### Fixed Variables

Fixed Variables are reserved variables that are populated by PEBakery and cannot be overwritten*.

_*The Winbuilder compatibility option `Overrideable Fixed Variables` may be enabled for compatibility with older projects in transition from Winbuilder to PEBakery, however it is recommended that the project be updated as quickly as possible to remove this unsafe behavior._

#### Fixed System Variables

| Variable | Description |
| --- | --- |
| %PEBakery% | Always returns `TRUE` if the script is running with PEBakery. Used for cross-builder compatibility with scripts containing features not implemented in Winbuilder.  |
| %BaseDir% | The directory where PEBakery was launched from. This variable is used extensively as a reference point for determining the relative paths of important directories such as  `Projects`, `Target`, and `Cache/Workbench`. Ex. `%BaseDir%\Target` |
| %Version% | For compatibility with scripts designed for Winbuilder this variable always returns `082`. |
| %EngineVersion% | Returns the machine friendly version of the PEBakery engine. |
| %PEBakeryVersion% | Returns the human friendly version of the PEBakery engine. |
| %ProjectTitle% | The name of the project as defined in script.projects `Main` section. |
| %ProjectDir% | The full path to the directory containing the project (script.project). |

#### Fixed Script Variables

| Variable | Description |
| --- | --- |
| %ScriptDir% | The full path to the directory containing the currently running script. |
| %ScriptFile% | The full path of the currently running script. |
| %ScriptTitle% | The title of the currently running script as defined by the script's `[Main]` section. |

#### Fixed Environment Variables

Fixed environment variables are included only for compatibility with Winbuilder and must be enabled with the compatibility option `Enable Environment Variables`. If you need to retrieve information about the local operating system's environment it is recommended to use the more flexible and accurate `System,GetEnv` command instead.

| Variable | Description |
| --- | --- |
| %ProcessorType% | One of the following: |
|| 586 - Intel-based 32-bit processor architecture. |
|| 8664 - Intel-based 64-bit processor architecture. |
|| Arm - 32-bit ARM processor architecture. **PEBakery Only** |
|| Arm64 - 64-bit ARM processor architecture. **PEBakery Only** |
|| Unknown - Any other architecture. |
| %ProgramFilesDir% | The path of the local operating system's `Program Files` directory. |
| %ProgramFilesDir_x86% | If The path of the local operating system's `Program Files (x86)` directory (x64 OS only). |
| %TempDir% | The path of the local operating system's `Temp` directory. |
| %UserName% | The name of the currently logged in user. |
| %UserProfile% | The path of the logged in user's home directory. |
| %WindowsDir% | The path of the local operating system's `Windows` directory. |
| %WindowsVersion% | The local operating system's version number. |

### Local Variables

Local variables are "visible" only to the currently running script. All variables are created in the local scope unless explicitly defined otherwise.

#### Reserved Local Variables

Some PEBakery commands return the status of various commands via pre-defined variables. It is advised not to use these variable names in your scripts in order to prevent them from being overwritten.

| Variable | Command | Description |
| --- | --- |
| %StatusCode% | [WebGet](.Commands/Network/WebGet.md) | Contains the HTTP Status code from the most recent WebGet operation. |
| %ExitCode% | [ShellExecute](.Commands/System/ShellExecute.md), [ShellExecuteDelete](.Commands/System/ShellExecuteDelete.md) | Contains the *Exit Code* returned by the most recent `ShellExecute` command. |

### Global Variables

Global variables are available to the entire project and can be defined by:

Script.Project's [Variables] section

```pebakery
[Variables]
%myVar%=12345
```

The `GLOBAL` keyword

```pebakery
Set,%myVar%,12345,GLOBAL
```

#### Legacy Global Variables

The following variables are included for compatibility with WinBuilder, which stores them in the `[Main]` section of `script.project`.

If `PathSetting=True` is defined in `script.project` then the following variables are set to the value of the matching key in `script.project's` `[Main]` section. If `PathSetting=False` they will be ignored.

| Variable | PathSetting | Value |
| --- | :---: | --- |
| %SourceDir% | True | Value of `SourceDir=` |
| | False | undefined |
| %TargetDir% | True | Value of `TargetDir=` |
| | False | undefined
| %ISOFile% | True | Value of `ISOFile=` |
| | False | undefined |

## Related

[AddVariables](/Commands/Control/AddVariables.md), [Set](/Commands/Control/Set.md), [Project Variables](/Projects/ProjectVariables.md), [Script Variables](/Projects/ScriptVariables.md)