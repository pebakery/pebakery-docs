# LoopEx

Loops through a series of commands based on the value of a counter.

`LoopEx` is an extended form of the standard `Loop` command that allows passing parameters by reference as well as by value.

## Syntax

```pebakery
LoopEx,<FileName>,<Section>,<StartValue>,<EndValue>[,Parameters]
```

```pebakery
LoopEx,BREAK
```

### Arguments

#### Version 1

| Argument | Description |
| --- | --- |
| FileName | The full path to the script containing the `Section` to execute. Hint: Use `%ScriptFile%` to reference the current script. |
| Section | The [Section] to execute. |
| StartValue | The initial value to start from. Each time the loop finishes the value will be incremented. |
| EndValue |  The final value to be reached by incrementing `StartValue`. Once this value is reached the loop stops. |
| Parameters | **(Optional)** Parameters to pass to the `Section` being executed. Parameters must be defined as either `In=` or `Out=`. |
|| `In=<%variable%>` - Pass by value. |
|| `Out=<%variable%>` - Pass by reference. If the variable does not exist it will be created. | 

#### Version 2

| Argument | Description |
| --- | --- |
| BREAK | Immediately exits the loop. The script will continue processing with the next line following the `LoopEx` command. |

### Variables

The following variables are passed by PEBakery and can be used to perform additional operations within the loop.

| Token | Description |
| --- | --- |
| `%^SIPARAM_1%`, `%^SIPARAM_2%`, `%^SIPARAM_3%`, etc. | Used within a `Section` to access any parameters passed. The numbering scheme starts from `1` and continues in the order the parameters were passed. These variables are discarded when the section is finished processing. |
| `%^SIPARAM_COUNT%` | Contains the number of parameters passed to `Section`. |
| `%^RET%` | Return a value from the `Section`. This token is not affected by the constraints of `System,SetLocal` and can be used to return the value of an isolated variable to the main process. `%^RET%` is volatile so if you need to preserve the return value copy it into a local variable. |
| `%^LOOP_IDX%` | Contains the current value of the loop relative to `StartValue` and `EndValue`. |
| `%^SOPARAM_1%`, `%^SOPARAM_2%`, `%^SOPARAM_3%`, etc.| References an `Out=` variable inside the called section. The numbering scheme starts from `1` and continues in the order the `Out=` parameters were passed. These variables are discarded when the section is finished processing. |

## Remarks

PEBakery allows an unlimited number of parameters to be passed to the `[section]` being executed.

Although the parameters themselves are passed by value using section variables, all variables are in the scope of the entire script, so the original values can modified by referencing them by name. If required, you can use the `System,SetLocal` command to isolate variables modified within the running section.

*Note:* Winbuilder allows looping through characters A-Z in addition to integers. The PEBakery `LoopLetter` and `LoopLetterEx` commands replaces this functionality. For backwards compatibility with legacy projects you can enable the _Allow Letter in Loop's Arugment_ compatibility option in PEBakery's settings.

## Related

[ForEach](./ForEach.md), [ForRange](./ForRange.md), [Loop](./Loop.md), [LoopLetter](./LoopLetter.md), [LoopLetterEx](./LoopLetterEx.md), [System,SetLocal](../System/SetLocal.md), [System,EndLocal](../System/EndLocal.md)

## Examples

### Example 1

A simple loop that counts to 10 and appends to a variable.

```pebakery
[main]
Title=LoopEx-Count Example
Description=Demonstrate LoopEx.
Level=5
Version=1
Author=Homes32

[variables]

[process]
LoopEx,%ScriptFile%,Count,1,10,Out=%Result%
Message,%Result%

[Count]
System,SetLocal
Set,%^SOPARAM_1%,"%^SOPARAM_1% %^LOOP_IDX%..."
System,EndLocal
```
