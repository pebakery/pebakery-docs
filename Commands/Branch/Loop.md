# Loop

Loops through a series of commands based on the value of a counter.

## Syntax

```pebakery
Loop,<FileName>,<Section>,<StartValue>,<EndValue>[,Parameters]
```

```pebakery
Loop,BREAK
```

### Arguments

#### Version 1

| Argument | Description |
| --- | --- |
| FileName | The full path to the script containing the `Section` to execute. Hint: Use %ScriptFile% to reference the current script. |
| Section | The [Section] to execute. |
| StartValue | The initial value to start from. Each time the loop finishes the value will be incremented. |
| EndValue |  The final value to be reached by incrementing `StartValue`. Once this value is reached the loop stops. |
| Parameters | **(Optional)** Parameters to pass to the `Section` being executed. |

#### Version 2

| Argument | Description |
| --- | --- |
| BREAK | Immediately exits the loop. The script will continue processing with the next line following the `Loop` command. |

### Tokens

The following tokens are passed by PEBakery and can be used to perform additional operations within the loop.

| Token | Description |
| --- | --- |
| #1, #2, #3, etc. | Used within a `Section` to access any parameters passed. The numbering scheme starts from `1` and continues in the order the parameters were passed. These tokens are discarded when the section is finished processing. |
| #a | Contains the number of parameters passed to `Section`. |
| #c | Contains the current value of the loop relative to `StartValue` and `EndValue`. |

## Remarks

PEBakery allows an unlimited number of parameters to be passed to the `[section]` being executed.

Although the parameters themselves are passed by value using tokens, all variables are in the scope of the entire script, so the original values can modified by referencing them by name. If required, you can use the `System,SetLocal` command to isolate variables modified within the running section.

*Note:* Winbuilder allows looping through characters A-Z in addition to integers. The PEBakery `LoopLetter` command replaces this functionality. For backwards compatibility with legacy projects you can enable the _Allow Letter in Loop's Arugment_ compatibility option in PEBakery's settings.

## Related

[LoopLetter](./LoopLetter.md), [System,SetLocal](../System/SetLocal.md), [System,EndLocal](../System/EndLocal.md)

## Examples

### Example 1

A simple loop that counts to 10 and displays a message box showing the current loop count.

```pebakery
[main]
Title=Loop-Count Example
Description=Demonstrate how to retrieve the count in a loop.
Level=5
Version=1
Author=Homes32

[variables]

[process]
Loop,%ScriptFile%,Count,1,10

[Count]
Message,"Count: #c"
```

### Example 2

We can also use Loop to quickly process a large number of interface controls. In the following example we have 10 input boxes representing file extensions we want to register. Instead of writing 10 `If,xxx,Equal,True,Run,%ScriptFile%,Process-Ext,xxx` statements we can do the same amount of work using only 2 lines of code. If we want to add more interface controls we only need create the control and increase our counter, making for a very small, fast script.

```pebakery
[main]
Title=Loop-Interface Example
Description=Demonstrate how to loop through interface controls.
Level=5
Version=1
Author=Homes32

[variables]

[process]
Loop,%ScriptFile%,Process-Ext,1,10

[Process-Ext]
// #c is the current value of our loop counter
If,%CB_Asso_#c%,Equal,True,Run,%ScriptFile%,Register-Ext,%IN_Asso_#c%

[Register-Ext]
// #1 is the 1st (and only) parameter we passed to
// this section and represents the value of the current input box
Echo,"Registering file extension [#1]..."

[Interface]
pTextLabel5_1="File associations:",1,1,9,21,99,18,8,Bold
CB_Asso_1=,1,3,11,46,20,20,True
IN_Asso_1=,1,0,31,46,50,20,txt
CB_Asso_2=,1,3,11,72,20,20,True
IN_Asso_2=,1,0,31,71,50,20,pdf
CB_Asso_3=,1,3,11,96,20,20,True
IN_Asso_3=,1,0,31,96,50,20,script
CB_Asso_4=,1,3,11,121,18,20,True
IN_Asso_4=,1,0,31,121,50,20,log
CB_Asso_5=,1,3,11,146,18,20,False
IN_Asso_5=,1,0,31,146,50,20,
CB_Asso_6=,1,3,11,171,20,20,True
IN_Asso_6=,1,0,31,171,50,20,exe
CB_Asso_7=,1,3,11,197,18,20,False
IN_Asso_7=,1,0,31,196,50,20,
CB_Asso_8=,1,3,11,222,18,20,False
IN_Asso_8=,1,0,31,221,50,20,
CB_Asso_9=,1,3,11,247,18,20,False
IN_Asso_9=,1,0,31,246,50,20,
CB_Asso_10=,1,3,11,272,18,20,False
IN_Asso_10=,1,0,31,271,50,20,
```

### Example 3

In this example we are searching in all *oem#.inf* files in path *C:\Windows\inf\* (oem0.inf up to oem100.inf) for the entry called *VBoxUSB.sys* in section *[SourceDisksFiles]*. If the entry is found the correct *oem#.inf* file name is saved to our result and the loop ends.

NOTE: oem.inf files alway begin with ZERO (oem0.inf).

```pebakery
[main]
Title=Loop-Ini-Search
Description=Demonstrate how to loop through files.
Level=5
Version=1
Author=Homes32

[variables]
%Result%="[Not Found]"

[process]
Loop,%ScriptFile%,Try-OEM,0,100,SourceDisksFiles,VBoxUSB.sys
Echo,Found VBoxUSB.sys in [%Result%]

[Try-OEM]
Set,%file%,C:\Windows\inf\oem#c.inf
If,ExistFile,%file%,IniRead,%file%,#1,#2,%var%
If,Not,-%var%,Equal,-,Begin
  Set,%Result%,%file%
  Loop,BREAK
End
```