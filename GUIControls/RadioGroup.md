# Radio Group Control

A group of radio buttons. Only one radio button per group may be selected at a time.

## Syntax

```pebakery
<Name>=<Caption>,<Visibility>,14,<PosX>,<PosY>,<Width>,<Height>,<Item1>,<Item2>,<ItemN>,<SelectedIndex>[,<SectionToRun>,<ShowProgress>][,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| Caption | Label displayed on the top of the radio group. Use `""` for none. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | `14` - The control ID specifying that this is a Radio Group. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| Items | Options to display in radio group. Multiple values are separated by commas. |
| SelectedIndex | Zero-based index of the selected `Item`. |
| SectionToRun | **(Optional)** Defines the [Section] within the script that will be processed when the button is pressed or the value of the control is changed. The section name must be enclosed in underscore `_` characters. *Example:* `_RunMe_` |
| ShowProgress | **(Optional)** True/False - Show the Build progress screen while `SectionToRun` is being executed. This argument must always follow the `SectionToRun` argument. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

## Remarks

The `Value` of the radio group can be read by referencing the control `Name` as a variable. Ex. `%RadioGroup1%` or by using the `ReadInterface` command.

## Related

[ReadInterface](../Commands/Interface/ReadInterface.md), [WriteInterface](../Commands/Interface/WriteInterface.md)

## Examples

```pebakery
// A RadioGroup called "Radio Group" with 3 choices. The choice "Option1" is selected.
RadioGroup1="Radio Group",1,14,433,115,90,69,Option1,Option2,Option3,1
```