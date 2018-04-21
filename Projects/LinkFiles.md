# .Link Files

`.Link` files are "symbolic links" used to include individual scripts from another location in a PEBakery project.

## File Location

The file must be located in a sub-folder of PEBakery's `Projects` directory.

```text
C:\PEBakery\
|--- Projects\
     |--- myProject\
     |--- Build\
              |---my.script
              |---myOtherScript.link
              |--- folder.project
     |--- Tools\
|--- Launcher.exe
|--- PEBakery.ini
```

## File Format

Link files are text files with the extension `.link` and are made up of "Sections" very similar to a standard _.ini_ file.

Unlike "folder links" defined by `folder.project` files, `.link` files store the selected state in the link file itself allowing a script linked to several project to be independently selected by each project.

## Sections

The structure of a link file consists of 1 major section. Additional sections may be defined by the project author but will be ignored by PEBakery. `[Interface]`, `[Process]`, and `[Variable]` sections are not supported.

While link files can technically contain code that can be executed with the `Run` or `Exec` commands, using link files as a code library is strongly discouraged.

### [Main]

The following values are used by PEBakery to define a link and it's behavior. Script developers may define additional values under the `[Main]` section for other uses. These values will be ignored by PEBakery.

| Name | Description |
| --- | --- |
| Link | The path to the .script file to include in the project. Paths are considered relative to the `%BaseDir%` unless an absolute path is specified. |
|Selected | **(Optional)** Defines how the script can be selected for processing. Default is True. |
|| True - The script is selected in the project tree and will be processed. |
|| False - The script is deselected in the project tree and will not be processed. |
|| None - The script is not allowed to be selected/deselected and will not be processed. Used primarily for configuration and utility scripts. |

## Remarks

With the exception of toggling the selected state via the Project Tree any changes made to a linked script will modify the original .script file.

## Related

[.Folder Files](./FolderFiles.md)

## Examples

### Example 1

This example links to several folders relative to the `%BaseDir%` (for this example this is assumed to be _C:\PEBakery\\_).

```pebakery
[Main]
Link=Projects\Addons\AccessGainDrivers.script
Selected=False
```

### Example 2

This example links to an absolute path.

```pebakery
[Main]
Link=C:\MyScripts\Addons\AccessGainDrivers.script
Selected=True
```