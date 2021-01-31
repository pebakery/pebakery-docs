# Script.Project Files

The `Script.Project` file defines a project.

Each project has one, and only one script.project file that may contain variables, macros, commands, encoded files, and possibly a Graphical User Interface (GUI) that make up the base of the project.

## File Location

The file must be located in a sub-folder (usually matching the `Title` of the project) of PEBakery's `Projects` directory.

```
C:\PEBakery\
|--- Projects\
     |--- myProject\
          |--- script.project
     |--- Tools\
|--- Launcher.exe
|--- PEBakery.ini
```

## File Format

Script.project files are text files with the name `script.project` and are made up of "Sections" very similar to a standard _.ini_ file. At a minimum a script.project file must contain a `Main` section that defines the `Title` of your project in order for it to appear in PEBakery's _Project Tree_. All .script files under the directory structure of script.project will be loaded as child nodes under the project `Title`.

## Sections

The structure of a script.project file consists of 4 major sections. Additional sections may be defined by the project author to included additional commands, interfaces, or embedded files.

### Main Sections

The following sections define the behavior and actions of the script. Click on a `Section` name for more details.

| Section | Description |
| --- | --- |
| [Main](./ProjectMain.md) | The main section that defines your script. |
| [Interface](./ScriptInterface.md) | **(Optional)** The Interface section contains one ore more lines that define the controls of a script's Graphical User Interface.  |
| [Process](./ProjectProcess.md) | **(Optional)** This sections contains the main logic of the script and is processed when you press the `Build` button. |
| [Variables](./ProjectVariables.md) | **(Optional)** This section is used to declare predefined variables and macros used by the script at runtime. |

### Internal Sections

The following sections are used internally by PEBakery and should not be modified.
For more details about encoded files see `Script Commands`.

| Section | Description |
| --- | --- |
| EncodedFolders | Contains a list of folders containing encoded files. |
| _\<FolderName>_ | Contains a list of files contained within the specified folder. |
| EncodedFile-_\<FolderName>_-_\<FileName>_ | Contains an encoded file. |
| InterfaceEncoded | Contains a list of encoded files used by the script's Graphical User Interface |
| EncodedFile-InterfaceEncoded-_\<FileName>_ | Contains the encoded file referenced by `FileName` from the `InterfaceEncoded` section. |
| AuthorEncoded | Defines the script's logo image. |
| EncodedFile-AuthorEncoded-_\<FileName>_ | Contains the encoded file for the script's logo image. |

## Remarks

None.

## Related

[Script Commands](../Commands/Script/README.md), [Script Files (.script)](./ScriptFiles.md)
