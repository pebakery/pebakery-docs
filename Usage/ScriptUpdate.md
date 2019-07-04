# Script Update

This sections controls how PEBakery will perform script updates.


Script updates are configured via the [ScriptUpdate](/Projects/ScriptUpdateScript.md) section in each individual script file.

The Update Process

1. Read the value of UpdateType [ScriptUpdate]
1. Read the value of URl from [ScriptUpdate]
1. Download scripts metadata from <url>/<scriptTitle>.meta.json
1. Read metadata to determin if an update is necessary. PEBakery compares the version number from the scripts `[Main]` section to the version property in the script's update configuration.
1. Backup the current scripts interface values.
1. Download the updated script to a temporary location.
1. Restore the scripts interface values to the best of our ability.