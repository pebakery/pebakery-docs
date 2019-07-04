# Sections

Sections are specific blocks of code or other information within a script file. In addition to containing data in .INI style `Key=Value` format, Sections can be executed as functions/procedures using commands such as `Run` and `Exec` and can accept parameters and return values as required.

## Defining a Section

Sections are defined by specifying the name of the section within `[]`brackets, (Ex.: `[mySection]`) and end when either another section starts or the "end of file" is reached.

## Examples

### Example 1

Multiple `Sections` within a script file.

```pebakery
[Main]
Title=Section Example 1
Description=Show how sections are defined.
Author=Homes32
Level=5
Version=1

[Variables]
%a%=1

[Process]
Run,%ScriptFile%,doSomething,one,two,three,four,five,six,seven,eight,nine,ten,eleven,twelve

[doSomething]
GetParam,12,%myParam%
Message,"Parameter 12: %myParam%"

[anotherSection]
// nothing to see here...

[Interface]
pFileBox1=C:\Images\,1,13,23,44,230,20,dir
pTextLabel1="Select your source directory:",1,1,23,25,230,18,8,Bold
```
