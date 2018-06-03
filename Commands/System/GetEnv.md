# System,GetEnv

Gets the value of environment variable from the host operating system.

## Syntax

```pebakery
System,GetEnv,<EnvVar>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| EnvVar | The name of the environment variable to read. Do **not** include surrounding `%` signs. |
| %DestVar% | The variable where the value of the environment variable will be stored. |

### Common Environment Variables

The following is a list of commonly used environment variables defined in modern versions of Microsoft Windows. A full list of environment variables in use on your system may be obtained by issuing the `set` command from the Windows Command Prompt.

| Environment Variable | Description |
| --- | --- |
| APPDATA | The path to the local users Application Data folder. Usually `C:\Users\%username&\AppData\Roaming`. |
| CommonProgramFiles | The path to the Common Files directory. Usually `C:\Program Files\Common Files`. |
| CommonProgramFiles(x86) | On 64bit operating systems this is the path to the folder containing 32bit Common Files. Usually `C:\Program Files (x86)\Common Files`. |
| COMPUTERNAME | The name of the computer. |
| NUMBER_OF_PROCESSORS | The number of processor cores in your CPU. |
| OS | Operating System Family. Ex. `Windows_NT`. |
| PROCESSOR_ARCHITECTURE | CPU Architecture. Ex. `x86` or `AMD64`. |
| ProgramData | The path to the folder containing Shared Application Data. Usually `C:\ProgramData`. |
| ProgramFiles | The path to the folder containing installed applications. Usually `C:\Program Files`. |
| ProgramFiles(x86) | On 64bit operating systems this is the path to the folder containing installed 32bit applications. Usually `C:\Program Files (x86)`. |
| SystemDrive | The drive letter where Windows is installed. Usually `C:` |
| SystemRoot | The directory where Windows is installed. Usually `C:\Windows`. |
| TEMP | The local user's temp directory. Usually `C:\Users\%username%\AppData\Local\Temp`. |
| USERNAME | The name of the current user. |
| USERPROFILE | The current user's home directory. Usually `C:\Users\%username%`. |
| windir | The Windows directory. Usually `C:\Windows`. |

## Remarks

If `EnvVar` does not exist `%DestVar%` will contain a blank value.

## Related

## Examples

### Example 1

```pebakery
[main]
Title=GetEnv Example
Description=Show usage of the System,GetEnv command.
Level=5
Version=1
Author=Homes32

[variables]

[process]
System,GetEnv,TEMP,%hostTemp%
System,GetEnv,PROCESSOR_ARCHITECTURE,%hostARCH%
Message,"#$pTEMP#$p = %hostTemp%#$x#$pPROCESSOR_ARCHITECTURE#$p = %hostARCH%",INFORMATION
```