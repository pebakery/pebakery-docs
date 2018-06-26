# Combo Box Control

A drop-down list allowing you to select a single value.

## Syntax

```pebakery
<Name>=<Value>,<Visibility>,4,<PosX>,<PosY>,<Width>,<Height>,<Item1>,<Item2>,<ItemN>[,<SectionToRun>,<ShowProgress>][,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| Value | The value currently selected by the combo box. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | `4` - The control ID specifying that this is a Combo Box. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| Items | Options to display in the combo box. Multiple values are separated by commas. |
| SectionToRun | **(Optional)** Defines the [Section] within the script that will be processed when the button is pressed or the value of the control is changed. The section name must be enclosed in underscore `_` characters. *Example:* `_RunMe_` |
| ShowProgress | **(Optional)** True/False - Show the Build progress screen while `SectionToRun` is being executed. This argument must always follow the `SectionToRun` argument. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

## Remarks

The `Value` of the combo box can be read by referencing the control `Name` as a variable. Ex. `%ComboBox1%` or by using the `ReadInterface` command.

## Related

[ReadInterface](/Commands/Interface/ReadInterface.md), [WriteInterface](/Commands/Interface/WriteInterface.md)

## Examples

```pebakery
// Combobox with 3 options
ComboBox1="Option 1",1,4,136,134,115,21,"Option 1","Option 2","Option 3"

// Combobox with 3 options that will run `mySection` when a value is changed
ComboBox2="Option 1",1,4,136,154,115,21,"Option 1","Option 2","Option 3",_mySection_,True
```