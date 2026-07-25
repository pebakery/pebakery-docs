# ExtractAndRun

Extracts a single file from inside a script and executes it.

## Syntax

```pebakery
ExtractAndRun,<ScriptFile>,<DirName>,<FileName>[,Parameters]
```

### Arguments

| Argument | Description |
| --- | --- |
| ScriptFile | The full path to the script. **Hint:** Use `%ScriptFile%` to reference the current script. |
| DirName | The folder inside the script that contains the file. |
| FileName | The name of the file to extract and execute. |
| Parameters | **(Optional)** Parameters to be passed to the executable. Parameters must not contain spaces, quotes or commas. Use the escaped form of these characters (i.e. #$s, #$q, #$c ) if needed. |

## Remarks

`FileName` is extracted to the a randomly named subdirectory under the %TEMP% directory defined by the OS (usually *C:\Users\username\AppData\Local\Temp*) and is deleted when execution terminates.

`FileName` is executed in the foreground and blocks the script from further action until the process terminates. If you require more control over the process's execution use the **ExtractFile** and **ShellExecute/ShellExecuteDelete** commands instead.

## Related

[Encode](./Encode.md), [ExtractAllFiles](./ExtractAllFiles.md), [ExtractFile](./ExtractFile.md)

## Examples

### Example 1

Simple directory structure inside a script.

```pebakery
root/
|--- Folder/
     |--- myApp.exe
     |--- myApp.ini
     |--- mySelfExtractingSFX.exe
|--- Reg/
     |--- mySettings.reg
|--- Help/
     |---readme.txt
|--- src/
     |---mySrc.au3
```

Extract readme.txt and open with the default .txt handler.

```pebakery
ExtractAndRun,%ScriptFile%,Help,readme.txt
```

### Example 2

Extract mySelfExtractingSFX.exe and execute with the */silent /dir="C:\Tools"* parameter.

```pebakery
ExtractAndRun,%ScriptFile%,Folder,mySelfExtractingSFX.exe,"/silent#$s/dir=C:\Tools"
```

### Example 3

The following method is a more flexible alternative to the ExtractAndRun command.

```pebakery
[main]
Title=ExtractAndRun Alternative
Description=Demonstrate how to replicate the behavior of ExtractAndRun command.
Level=5
Version=1
Author=Homes32

// Define our Marco
[Variables]
ExtractAndRunEx=Run,%ScriptFile%,ExtractAndRunEx,%^SIPARAM_1%,%^SIPARAM_2%,%^SIPARAM_3%,%^SIPARAM_4%,%^SIPARAM_5%

[process]
ExtractAndRunEx,%ScriptFile%,Folder,myApp.exe

[ExtractAndRunEx]
// Syntax: ExtractAndRunEx,<Action>,<ScriptFile>,<DirName>,<FileName>,[,<Parameters>]
// %^SIPARAM_1% = Action (Open/Hide)  %^SIPARAM_2% = ScriptFile  %^SIPARAM_3% = DirName  %^SIPARAM_4% = FileName  %^SIPARAM_5% = Parameters
ExtractFile,%^SIPARAM_2%,%^SIPARAM_3%,%^SIPARAM_4%,%ProjectTemp%\
ShellExecuteDelete,%^SIPARAM_1%,%ProjectTemp%\%^SIPARAM_4%,%^SIPARAM_5%,%ProjectTemp%
```
