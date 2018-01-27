# Hash

Calculates the cryptographic hash of a file. 

The result can then be compared with a known value in order to verify the integrity of a file.

## Syntax

```pebakery
Hash,<HashType>,<FilePath>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| HashType | Hash type to calculate. Supported algorithms are: `MD5`, `SHA1`, `SHA256`, `SHA384`, `SHA512`.
| FilePath | The full path of file to hash. |
| DestVar | The variable where the hash digest will be saved. |

## Remarks

The `WebGet` command has hash verification of downloaded files builtin.

## Related

## Examples

### Example 1

The following example uses the `Hash` function to verify that *notepad.exe* is not corrupt.

```pebakery
[Main]
Title=Hash Example
Description=Show usage of the Hash Command
Author=Homes32
Level=5
Version=1

[Variables]
%notepadHash%=233a35e4b579ccde25951f8e543f1d16ae3e7b5b3f29c1d56e691ffb075ced15

[Process]
Hash,SHA256,%WindowsDir%\System32\notepad.exe,%Hash%
If,%Hash%,Equal,%notepadHash%,Message,"Notepad.exe verified!#$x#$xHash: %Hash%"
Else,Message,"Notepad.exe verification failed!#$x#$xHash: %Hash%#$x#$xdoes not match#$x#$x%notepadHash%"
```