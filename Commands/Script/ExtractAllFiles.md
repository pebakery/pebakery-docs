# ExtractAllFiles

Extracts all files from the specified directory inside a script.

## Syntax

```pebakery
ExtractAllFiles,<ScriptFile>,<DirName>,<DestDir>
```

### Arguments

| Argument | Description |
| --- | --- |
| ScriptFile | The full path to the script. **Hint:** Use `%ScriptFile%` to reference the current script. |
| DirName | The folder inside the script that contains the files. |
| DestDir | The full path of the target directory. If the files to be extracted already exist they will be overwritten. |

## Remarks

None.

## Related

[Encode](./Encode.md), [ExtractFile](./ExtractFile.md)

## Examples

### Example 1

Simple directory structure inside a script.

```pebakery
root/
|--- Folder/
     |--- myApp.exe
     |--- myApp.ini
     |--- moreFiles.7z
|--- Reg/
     |--- mySettings.reg
|--- src/
     |---mySrc.au3
```

Extract all files contained in the *Folder* directory of the running script to C:\Temp.

```pebakery
ExtractAllFiles,%ScriptFile%,Folder,C:\Temp
```