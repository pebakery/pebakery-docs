# Script Update

**Warning: Update functionality is in active development and may change without notice!**

PEBakery contains built-in update functionality for scripts that can be used by individual developers and project authors alike. It is triggered by the "Script update" button.

## Update Configuration

Script updates are configured via the [[UpdateScript]](../Projects/ScriptUpdateScript.md) section in each individual script file.

### Update Metadata

In order to reduce network bandwidth, information about the script on the update server is contained in a file called `<scriptTitle>.meta.json`. The meta-data file is in standard JSON format and contains information needed by the update process, such as the script's version, and any required dependencies.

More information about the `meta.json` file and the information it contains can be found in the [Update Server](./UpdateServer.md) guide.

## The Update Process

When the Script Update button is pressed PEBakery performs the following steps to determine if/how the script needs to be updated.

1. Read the value of UpdateType from the script's `[UpdateScript]` section.
1. Read the value of URl from the scrip's `[UpdateScript]` section.
1. Download script's meta-data from `<url>/<scriptTitle>.meta.json`.
1. Read the script's meta-data to determine if an update is necessary. PEBakery compares the version number from the scripts `[Main]` section to the version property in the script's update configuration.
1. Backup the current script's interface values.
1. Download the new script to a temporary location.
1. Upon successful download the old script is removed and the new script copied in it's place.
1. Restore the script's previous interface values to the best of our ability.