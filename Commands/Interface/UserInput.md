# UserInput

**Alias**: `Retrieve,Dir` `Retrieve,File`

Prompts the user to select a file or directory path.

## Syntax

```pebakery
UserInput,<BrowserType>,<InitPath>,<%DestVar%>[,Title=<Text>][,Filter=<FilterString>]
```

### Arguments

| Argument | Description |
| --- | --- |
| BrowserType | One of the following types: |
|| FilePath - Display a File Browser. |
|| DirPath - Display a Directory Browser. |
| InitPath | The starting path for the browse dialog. Leave blank `""` to let Windows choose the initial directory. |
| %DestVar% | The variable that will contain the full path of the selected file or directory. |
| Title= | **(Optional)** Text that will be displayed in the dialog title bar. **(Default)** If this argument is not defined the title bar will display `Open` (FilePath) or `Select Folder` (DirPath). |
| Filter= | **(Optional)** A filter string used to restrict the file type. **(File Browser Only)** |

## File Filter

There are two ways to restrict the file type a user may choose when presented with a file path dialog.

If no filter options are defined the default filter of `All Files|*.*` will be used.

### (Legacy) Winbuilder Style Filter

You may force the user to pick a specific file type (ie. a .txt file) by specifying the file extension in `InitPath`.

The filter must be in the format of `<Dir>\*.<Ext>` where *Ext* is the file extension allowed.

Example: `UserInput,FilePath,C:\*.txt,%var%`

Multiple file type filters are not supported.

### PEBakery Filter

You may force the user to pick from specific file types (ie. *.ini;*.txt;*.cfg file) by specifying `Filter=` argument.

For each filtering option, the filter string contains a description of the filter, followed by the vertical bar (|) and the filter pattern. The strings for different filtering options are separated by the vertical bar.

The following is an example of a filter string:

`Text files|*.txt|All files|*.*`

You can add several filter patterns to a filter by separating the file types with semicolons, for example:

`Image Files(*.BMP;*.JPG;*.GIF)|*.BMP;*.JPG;*.GIF|All files (*.*)|*.*`

The filter order is defined by the order of the filter list, therefore the first filter in the list will be the default selected filtering option.

If `Filter=` is defined any Winbuilder style filters will be ignored.

## Remarks

If the user clicks the cancel button on the browser dialog the operation will fail. You may use `System,ErrorOff` to prevent the build from Halting.

## Related

## Examples

### Example 1

```pebakery
[main]
Title=UserInput Example
Description=Show usage of the UserInput command.
Level=5
Version=1
Author=Homes32

[variables]

[process]
// File Browser allowing the user to pick any file type.
UserInput,FilePath,C:\,%var%
Message,"You selected: %var%"

// File Browser using the legacy Winbuilder style filter to only allow the user to pick .txt files.
UserInput,FilePath,C:\*.txt,%var%
Message,"You selected: %var%"

// File Browser using the `Filter=` argument to only allow the user to pick ini/cfg files by default.
UserInput,FilePath,"",%var%,"Filter=Config Files|*.ini;*.cfg|All Files|*.*"
Message,"You selected: %var%"

// Directory Browser with no starting folder defined.
UserInput,DirPath,"",%var%
Message,"You selected: %var%"

// Directory Browser
UserInput,DirPath,C:\,%var%,"Title=Please select a directory..."
Message,"You selected: %var%"
```