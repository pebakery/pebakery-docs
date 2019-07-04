# Script Update

Script updates are configured via the [[UpdateScript]](/Projects/ScriptUpdateScript.md) section in each individual script file.

The Update Process

1. Read the value of UpdateType [UpdateScript]
1. Read the value of URl from [UpdateScript]
1. Download scripts meta-data from <url>/<scriptTitle>.meta.json
1. Read meta-data to determine if an update is necessary. PEBakery compares the version number from the scripts `[Main]` section to the version property in the script's update configuration.
1. Backup the current scripts interface values.
1. Download the updated script to a temporary location.
1. Restore the scripts interface values to the best of our ability.