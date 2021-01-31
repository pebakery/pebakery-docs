# Check Box Control

A box that can be “checked” or “unchecked”.

## Syntax

```pebakery
<Name>=<Caption>,<Visibility>,3,<PosX>,<PosY>,<Width>,<Height>,<Value>[,<SectionToRun>,<ShowProgress>][,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| Caption | Label displayed next to the check box. Use `""` for none. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | `3` - The control ID specifying that this is a Check Box. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| Value | True/False - Checked `True` Unchecked `False` |
| SectionToRun | **(Optional)** Defines the [Section] within the script that will be processed when the button is pressed or the value of the control is changed. The section name must be enclosed in underscore `_` characters. *Example:* `_RunMe_` |
| ShowProgress | **(Optional)** True/False - Show the Build progress screen while `SectionToRun` is being executed. This argument must always follow the `SectionToRun` argument. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

## Remarks

The `Value` of the check box can be read by referencing the control `Name` as a variable. Ex. `%CheckBox1%` or by using the `ReadInterface` command.

## Related

[ReadInterface](../Commands/Interface/ReadInterface.md), [WriteInterface](../Commands/Interface/WriteInterface.md)

## Examples

```pebakery
// Checkbox in the "unchecked" (False) state
CheckBox1=CheckBox,1,3,137,110,104,20,False
```