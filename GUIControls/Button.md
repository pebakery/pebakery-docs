# Button Control

A simple button that can be used to run a section of code within the script.

## Syntax

```pebakery
<Name>=<Caption>,<Visibility>,8,<PosX>,<PosY>,<Width>,<Height>,<SectionToRun>,<Image>,<ShowProgress>[,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| Caption | The text shown on the button. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | `8` - The control ID specifying that this is a Button. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| SectionToRun | Defines the [Section] within the script that will be processed when the button is pressed. The specified section must reside within the current script. |
| Image | The name of the encoded image to display on the control. Use `0` for no image. |
| ShowProgress | True/False - Show the *Build progress* screen while `SectionToRun` is being executed. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

## Remarks

Buttons created with Winbuilder 082's internal interface editor have additional arguments including duplicate parameters for `_SectionToRun_` and `ShowProgress`. These fields are ignored by PEBakery. See Example 2.

Some buttons created in older versions of Winbuilder's internal interface editor omit the `Image` argument **and** suffers from duplicate `_SectionToRun_` and `ShowProgress` parameters. In this case you must update the control to include a value of `0` for the image argument.

## Related

[ReadInterface](/Commands/Interface/ReadInterface.md), [WriteInterface](/Commands/Interface/WriteInterface.md)

## Examples

### Example 1

```pebakery
// Button without image
Button1=Button,1,8,361,27,98,25,pButton1,0,False
// Button with image
Button2="Image Button",1,8,360,66,99,25,pButton2,tools.bmp,False
```

### Example 2

The following is an example of a button control that was generated using Winbuilder's built-in interface editor.

```pebakery
// Name=<Caption>,<Visibility>,8,<PosX>,<PosY>,<Width>,<Height>,<SectionToRun>,<Image>,<ShowProgress>,<False>,<_SectionToRun_>,<ShowProgress>,<__ToolTip>
pButton2="Button 2",1,8,23,75,80,25,runMe,tools.bmp,True,False,_runMe_,True,"__Launch this program."
```

#### Caveats

Parameter #11 is always created by Winbuilder's interface editor with a value of `False` but it is not used by either Winbuilder or PEBakery. Winbuilder 077b2 through 078 used parameter #11 for for the button's tooltip before the universal `__Tooltip` syntax was implemented.

Winbuilder's interface editor creates parameters #12 and #13 for `_SectionToRun_,ShowProgress`  but doesn't actually use them, instead referencing parameters #8 and #10.

#### Cleanup & Migration

When migrating scripts to PEBakery it is safe (and backwards compatible with Winbuilder) to remove all parameters after #10, unless the parameter begins with a double underscore eg. `__SomeText` indicating it's a tooltip.

In this example the above button definition can be simplified to:

```pebakery
// with tooltip
pButton2="Button 2",1,8,23,75,80,25,runMe,tools.bmp,True,"__Launch this program."

//without tooltip
pButton2="Button 2",1,8,23,75,80,25,runMe,tools.bmp,True
```
