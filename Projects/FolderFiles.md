# Folder.Project Files

`Folder.Project` files define additional properties and behavior for folders in PEBakery.

## File Location

The file must be located in a sub-folder of PEBakery's `Projects` directory.

```text
C:\PEBakery\
|--- Projects\
     |--- myProject\
     |--- Build\
              |---my.script
              |---folder.project
              |--- folder.project
     |--- Tools\
|--- Launcher.exe
|--- PEBakery.ini
```

## File Format

Folder.project files are text files with the name `folder.project` and are made up of "Sections" very similar to a standard _.ini_ file.

## Sections

The structure of a folder.project file consists of 1 major section. Additional sections may be defined by the project author but will be ignored by PEBakery. `[Interface]`, `[Process]`, and `[Variable]` sections are not supported.

While `Folder.project` files can technically contain code that can be executed with the `Run` or `Exec` commands, using `Folder.Project` files as a code library is strongly discouraged.

### [Links]

Contains a list of paths to import. Multiple paths may be specified, one per line. Link paths are considered to be relitive to the `%BaseDir%` unless an absolute path is specified.

All scripts in the specified folder and any sub-folders will be added to the folder containing the `folder.project` file. If any linked scripts are disabled then that script will also be disabled in the source project. Wildcard characters `*.*` at the end of the path are supported for compatibility with Winbuilder but are not required.

## Remarks

Any changes made to a linked script will modify the original .script file.

## Related

[.Link Files](./LinkFiles.md)

## Examples

### Example 1

This example links to several folders relative to the `%BaseDir%` (for this example this is assumed to be _C:\PEBakery\\_).

```pebakery
[Links]
Projects\Win10PESE\Apps\File Tasks
Projects\Win10PESE\Apps\HD Tasks\*.*
```

### Example 2

This example links to an absolute path.

```pebakery
[Links]
D:\MyScripts
C:\PEBakery\Projects\Win10PESE\Apps\HD Tasks\*.*
```
