# Path Box Control

An read-only input box with a browse button that allows you to select a file or directory.

PathBox is similar to the FileBox control with the difference being that PathBox does not allow editing the path directly; the user must select the file/dir with the browse button. PathBox also allows for processing a [Section] within the script when the value is changed. 

## Syntax

```pebakery
<Name>=<Value>,<Visibility>,20,<PosX>,<PosY>,<Width>,<Height>,<Type>,[Title=<String>][,Filter=<FilterString>][,<SectionToRun>,<ShowProgress>][,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| Value | The path currently entered in the Path Box. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | `20` - The control ID specifying that this is a Path Box. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| Type   | **(Optional)** Dialog type must be one of the following: |
|| `DIR` - **(Default)** The browse button will display a directory selection dialog. |
|| `FILE` - The browse button will display a file selection dialog. |
| Title= | **(Optional)** Text that will be displayed in the dialog title bar. **(Default)** |
| Filter= | **(Optional)** A filter string used to restrict the file type a user may choose. **(File Browser Only)** |
| SectionToRun | **(Optional)** Defines the [Section] within the script that will be processed when the value of the control is changed. The section name must be enclosed in underscore `_` characters. *Example:* `_RunMe_` |
| ShowProgress | **(Optional)** True/False - Show the Build progress screen while `SectionToRun` is being executed. This argument must always follow the `SectionToRun` argument. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

Optional arguments may be specified in any order.

## File Filter

You may force the user to pick from specific file types (ie. *.ini;*.txt;*.cfg file) by specifying `Filter=` argument.

For each filtering option, the filter string contains a description of the filter, followed by the vertical bar (|) and the filter pattern. The strings for different filtering options are separated by the vertical bar.

The following is an example of a filter string:

`Text files|*.txt|All files|*.*`

You can add several filter patterns to a filter by separating the file types with semicolons, for example:

`Image files|*.BMP;*.JPG;*.GIF|All files (*.*)|*.*`

The filter order is defined by the order of the filter list, therefore the first filter in the list will be the default selected filtering option.

## Remarks

The `Value` of the File Box can be read by referencing the control `Name` as a variable. Ex. `%PathBox1%` or by using the `ReadInterface` command.

`SectionToRun` will not be processed when the Clear button on the control or the Cancel button on the dialog is pressed.

## Related

[FileBox](./FileBox.md), [ReadInterface](../Commands/Interface/ReadInterface.md), [WriteInterface](../Commands/Interface/WriteInterface.md)

## Examples

```pebakery
// Select a file
PathBox01=PathBox01,1,20,10,10,200,20,file,"Title=select a file"
// Select a file, using the `Filter` argument to only allow the user to pick ini/cfg files by default.
PathBox02=PathBox02,1,20,10,40,200,20,file,"Filter=Config Files|*.ini;*.cfg|All Files|*.*"
// Select a directory
PathBox03=PathBox03,1,20,10,70,200,20,dir
// Select a directory and run the [RunMe] section when the value changes
PathBox04=PathBox04,1,20,10,100,200,20,dir,"Title=select a directory",_RunMe_,True
```