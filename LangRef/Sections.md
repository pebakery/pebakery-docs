# Sections

Sections are specific blocks of code or other information within a script file. In addition to containing data in .INI style `Key=Value` format, Sections can be executed as functions/procedures using commands such as `Run` and `Exec` and can accept parameters and return values as required.

## Defining a Section

Sections are defined by specifying the name of the section within `[]`brackets, (Ex. `[mySection]`) and end when either another section starts or the "end of file" is reached.

## Section Parameters

When used in conjunction with the `Run`, `Exec`, `SetMacro`, and similar commands sections can behave like a function and accept an unlimited number of parameters. 

To access a parameter that has been passed to a section you can:

- Access the parameter directly via it's reserved variable. (e.g `%^SIPARAM_1%`)
- Retrieve the parameter with `GetParam` based on it's position and assign it to a custom variable. (e.g. `GetParam,2,%Arg2%`) 

### Variables

The following reserved variables can be used to perform additional operations when executing a section.

| Variable | Description |
| --- | --- |
| `%^SIPARAM_1%`, `%^SIPARAM_2%`, `%^SIPARAM_3%`, etc. | Used within a `Section` to access any parameters passed. The numbering scheme starts from `1` and continues in the order the parameters were passed. These variables are discarded when the section is finished processing. |
| `%^SOPARAM_1%`, `%^SOPARAM_2%`, `%^SOPARAM_3%`, etc.| References an `Out=` variable inside the called section. The numbering scheme starts from `1` and continues in the order the `Out=` parameters were passed. These variables are discarded when the section is finished processing. |
| `%^SIPARAM_COUNT%` | Contains the number of parameters passed to `Section`. |
| `%^RET%` | Return a value from the `Section`. This variable is not affected by the constraints of `System,SetLocal` and can be used to return the value of an isolated variable to the main process. `%^RET%` is volatile so if you need to preserve the return value copy it into a local variable. |

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
