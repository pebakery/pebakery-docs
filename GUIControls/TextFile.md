# Text File Control

Displays a text file embedded within the script.

## Syntax

```pebakery
<Name>=<FileName>,<Visibility>,6,<PosX>,<PosY>,<Width>,<Height>[,<ToolTip>]
```

### Arguments

| Argument | Description |
| --- | --- |
| Name | Unique name used to reference this control. |
| FileName | The name of the encoded file to display. |
| Visibility | `True`/`False` - Show or Hide the control. |
| ControlID | `6` - The control ID specifying that this is a Text File. |
| PosX | Horizontal Position measured from the control's top left corner. |
| PosY | Vertical Position measured from the control's top left corner. |
| Width | Width of the control. |
| Height | Height of the control. |
| ToolTip | **(Optional)** Help Text that will be shown when the user hovers over the control. This argument must always begin with a double underscore `__`. *Example:* `"__Some useful info"` |

## Supported File Types

The TextFile control is capable of displaying rich text and plain text. 

Supported file types are:

TXT, RTF

Text based files with alternate file extensions (ex. CFG, CONF, INI, INF, LOG, SCRIPT) are also supported.

## Remarks

Text files are encoded and embedded in the script's `InterfaceEncoded` folder.

## Related

[ReadInterface](/Commands/Interface/ReadInterface.md), [WriteInterface](/Commands/Interface/WriteInterface.md)

## Examples

```pebakery
[Interface]
TextFile1=TextFile.txt,1,6,135,209,175,76

[InterfaceEncoded]
TextFile.txt=99,132

[EncodedFile-InterfaceEncoded-TextFile.txt]
lines=0
0=eJzzSM3JyVcIzy/KSVHk5fIgiwcA61sVjnic4wlJrShxy8xJ1SupKGEYBSMNuEBpSRzyN1W/mTEwAQAtYwdJj9s6pwEAAAACAAAAJgAAABkAAAAAAAAAAQAAAAAAAAAAAAAA
```