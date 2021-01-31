# General Settings

Settings related to the general behavior of the PEBakery engine.

## Settings

General settings may be configured via the **PEBakery > Settings > General** tab or by manually editing `PEBakery.ini` located in PEBakery's root directory *(eg. C:\PEBakery\PEBakery.ini)*.

### Build

| Setting | Default | Description |
| --- | --- | --- |
| [Optimize code](../CodingGuide/CommandOp.md) | True | Allows PEBakery to automatically optimize some commands related to file manipulation. |
| Show LogWindow after build | True | Show the log dialog when a build finishes. |
| Stop build on error | True | When enabled the build will halt on all errors. |

### Advanced

| Setting | Default | Description |
| --- | --- | --- |
| Enable long file path support | False | Allow PEBakery to override the Windows 260 character path limit and recognize filenames up to 32767 characters. **Warning:** Enabling this option can have unintended side affects. See [PEBakery Issue #135](https://github.com/pebakery/pebakery/issues/135) for details. |
| Enable update server management | False | Enable the ability to create script meta files. These files are used by PEBakery's internal script updater. See [Update Server](./UpdateServer.md) for details. |

### User-Agent

| Setting | Default | Description |
| --- | --- | --- |
| Custom User-Agent for WebGet | False | Allows you to override the default user-agent string (`PEBakery/<Version>`) used in WebGet operations. |