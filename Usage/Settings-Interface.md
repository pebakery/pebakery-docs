# Interface Settings

Settings related to the PEBakery's graphical user interface.

## Settings

Interface settings may be configured via the **PEBakery > Settings > Interface** tab or by manually editing `PEBakery.ini` located in PEBakery's root directory *(eg. C:\PEBakery\PEBakery.ini)*.

### PEBakery Interface

| Setting | Default | Description |
| --- | --- | --- |
| Display console output in ShellExectue | True | When enabled the build process will display the output from programs executed with `ShellExecute,Hide` in the progress window. |
| Custom Title | False | Allows you to change the caption on PEBakery's main window. |
| Interface Size | Adaptive | Configures the interface resizing method. |
| | Adaptive | Automatically scale PEBakery's top menu based on the screen resolution. |
| | Standard | Force PEBakery's top menu to use standard size buttons. |
| | Small | Force PEBakery's top menu to use small buttons. |
| Script Scale Factor (%) | 100% | Adjust the scaling of the scripts interface. |
| Monospaced Font | Configure the font used by PEBakery. |

### Path Length Limit

| Setting | Default | Description |
| --- | --- | --- |
| Enable long file path support | False | Allow PEBakery to override the Windows 260 character path limit and recognize filenames up to 32767 characters. |

### User-Agent

| Setting | Default | Description |
| --- | --- | --- |
| Custom User-Agent for WebGet | False | Allows you to override the default user-agent string used in WebGet operations. |