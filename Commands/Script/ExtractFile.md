# ExtractFile

Extracts a single file from inside a script.

## Syntax

```pebakery
ExtractFile,<ScriptFile>,<DirName>,<FileName>,<DestDir>
```

### Arguments

| Argument | Description |
| --- | --- |
| ScriptFile | The full path to the script. **Hint:** Use `%ScriptFile%` to reference the current script. |
| DirName | The folder inside the script that contains the file. |
| FileName | The name of the file to extract. |
| DestDir | The full path of the target directory. If `FileName` already exists it will be overwritten. |

## Remarks

None.

## Related

[Encode](./Encode.md), [ExtractAllFiles](./ExtractAllFiles.md)

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

Extract mySettings.reg from the running script's *Reg* directory.

```pebakery
ExtractFile,%ScriptFile%,Reg,mySettings.reg,c:\Temp
```