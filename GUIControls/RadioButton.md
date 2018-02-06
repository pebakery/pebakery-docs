# Radio Button Control

A circular button that can have only one radio button selected on the interface at a time.

## Syntax

```pebakery
<Name>=<Caption>,<Visibility>,11,<PosX>,<PosY>,<Width>,<Height>,<Value>[,<SectionToRun>,<ShowProgress>][,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| Caption | Label displayed next to the radio button. Use `""` for none. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | `11` - The control ID specifying that this is a Radio Button. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| Value | True/False - Selected `True` Deselected `False` |
| SectionToRun | **(Optional)** Defines the [Section] within the script that will be processed when the button is pressed or the value of the control is changed. The section name must be enclosed in underscore `_` characters. *Example:* `_RunMe_` |
| ShowProgress | **(Optional)** True/False - Show the Build progress screen while `SectionToRun` is being executed. This argument must always follow the `SectionToRun` argument. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

## Remarks

## Related

[ReadInterface](/Commands/Interface/ReadInterface.md), [WriteInterface](/Commands/Interface/WriteInterface.md)

## Examples

```pebakery
RadioButton1=RadioButton1,1,11,324,124,100,20,True
RadioButton2=RadioButton2,1,11,324,144,100,20,False
RadioButton3=RadioButton3,1,11,324,164,100,20,False
```