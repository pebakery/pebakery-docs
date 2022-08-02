# Interface Settings

Settings related to the PEBakery's graphical user interface.

## Settings

Interface settings may be configured via the **PEBakery > Settings > Interface** tab or by manually editing `PEBakery.ini` located in PEBakery's root directory *(eg. C:\PEBakery\PEBakery.ini)*.

### PEBakery Interface

| Setting | Default | Description |
| --- | --- | --- |
| Display console output in ShellExectue | True | When enabled the build process will display the output from programs executed with `ShellExecute,Hide` in the progress window. StdOut will be displayed in black text, StdErr will be displayed in red text. |
| Custom Title | False | Allows you to change the caption on PEBakery's main window. |
| Interface Size | Adaptive | Configures the interface resizing method. |
| | Adaptive | Automatically scale PEBakery's top menu based on the screen resolution. |
| | Standard | Force PEBakery's top menu to use standard size buttons. |
| | Small | Force PEBakery's top menu to use small buttons. |
| Script Scale Factor (%) | 100% | Adjust the scaling of the scripts interface. |
| Monospaced Font | Configure the font used by various portions of PEBakery. (ShellExecute output, combobox, codebox, etc.) |

### External Code Editor

| Setting | Default | Description |
| --- | --- | --- |
| Custom Editor | False | Allows you to specify the program used to edit the script source. If this option is disabled PEBakery will attempt to launch an editor using the current operating system's default file associations. |
