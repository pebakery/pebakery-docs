# GetParam

Retrieves parameters passed to a section and convert them into variables.

## Syntax

```pebakery
GetParam,<Index>,<%Variable%>
```

### Arguments

| Argument | Description |
| --- | --- |
| Index | The 1-based index of the parameter to retrieve. |
| %Variable% | The name of variable where the value will be saved. |

## Remarks

As a result of PEBakery's backwards compatible Winbuilder syntax, parameters passed to a section can only be referenced by tokens consisting of a hash mark `#` followed by a single digit representing the 1-base index of the parameter (ex. #1). The `GetParam` command must be used to retrieve the value of any parameter index greater then 9.

## Related

[Sections](../../LangRef/Sections.md)

## Examples

Using `GetParam` to retrieve the value of the 12th parameter passed to a section.

### Example 1

```pebakery
[Main]
Title=GetParam Example 1
Description=Show usage of the GetParam command.
Author=Homes32
Level=5
Version=1

[Variables]

[Process]
Run,%ScriptFile%,doSomething,one,two,three,four,five,six,seven,eight,nine,ten,eleven,twelve

[doSomething]
GetParam,12,%myParam%
Message,"Parameter 12: %myParam%"

[Interface]
pFileBox1=C:\Images\,1,13,23,44,230,20,dir
pTextLabel1="Select your source directory:",1,1,23,25,230,18,8,Bold
```

### Example 2

Using GetParam can also be an easy way to make your code more readable, since it allows you to assign a meaningful variable name to the parameters, especially when you have many of them.

```
GetParam,5,%SomeValue%
If,%SomeValue%,Equal,True,Run,%ScriptFile%,DoSomething
````

is more easily understood then

`If,#5,Equal,True,Run,%ScriptFile%,DoSomething`