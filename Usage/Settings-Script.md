# Script Settings

Settings related to PEBakery's script handling.

## Settings

Script settings may be configured via the **PEBakery > Settings > Script** tab or by manually editing `PEBakery.ini` located in PEBakery's root directory *(eg. C:\PEBakery\PEBakery.ini)*.

### Script Cache

| Setting | Default | Description |
| --- | --- | --- |
| Enable script cache | True | When enabled PEBakery serializes and caches all scripts in a SQLLite database (located in `%BaseDir%\Database`) in order to improve load times. |
| Clear Cache | | Pressing this button clears the database. The script cache will be rebuilt when the project is Refreshed. |

### Syntax Check

| Setting | Default | Description |
| --- | --- | --- |
| Auto check syntax errors | True | Automatically check scripts for syntax errors. |