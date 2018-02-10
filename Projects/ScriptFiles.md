# .Script Files

.Script files are the building blocks of a project and contain the commands and logic needed to build your PE.

Each .script file may contain variables, macros, commands, encoded files, and possibly a Graphical User Interface (GUI) that work together to perform various tasks; from building the core of the project to adding additional applications and configuring settings.

The file must be located in PEBakery’s `Projects` directory, under the respective project folder.

## File Format

.Script files are text files with a `.script` extension and are made up of "Sections" very similar to a standard _.ini_ file. At a minimum a .script file must contain a `Main` section that defines the `Title` and `Level` of your script in order for it to appear in PEBakery's _Project Tree_.

## Sections

The structure of a .script file consists of 4 major sections. Additional sections may be defined by the script author to included additional commands, interfaces, or embedded files.

### Main Sections

The following sections define the behavior and actions of the script. Click on a `Section` name for more details.

| Section | Description |
| --- | --- |
| [Main](./ScriptMain.md) | The main section that defines your script. |
| [Interface](./ScriptInterface.md) | **(Optional)** The Interface section contains one ore more lines that define the controls of a script's Graphical User Interface.  |
| [Process](./ScriptProcess.md) | **(Optional)** This sections contains the main logic of the script and is processed when you press the `Build` button. |
| [Variables](./ScriptVariables.md) | **(Optional)** This section is used to declare predefined variables and macros used by the script at runtime. |

### Internal Sections

The following sections are used internally by PEBakery and should not be modified.
For more details about encoded files see `Script Commands`.

| Section | Description |
| --- | --- |
| EncodedFolders | Contains a list of folders containing encoded files. |
| _<FolderName>_ | Contains a list of files contained within the specified folder. |
| EncodedFile-_<FolderName>_-_<FileName>_ | Contains an encoded file. |
| InterfaceEncoded | Contains a list of encoded files used by the script's Graphical User Interface |
| `EncodedFile-InterfaceEncoded-<FileName>` | Contains the encoded file referenced by `FileName` from the `InterfaceEncoded` section. |
| AuthorEncoded | Defines the script's logo image. |
| `EncodedFile-AuthorEncoded-<FileName>` | Contains the encoded file for the script's logo image. |

## Remarks

None.

## Related

[Project File (script.project)](./ProjectFiles.md)