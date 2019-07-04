# Update Server

**Warning: Update functionality is in active development and may change without notice!**

## Update (Meta.json) Schema

As of Schema v0.1 the following meta-data fields are supported in the meta.json file.

### Main Object

| Property| Description |
| --- | --- |
| meta_schema_ver | The version of the schema used for this meta.json file. PEBakery uses this information to determin which data values are supported. |
| pebakery_min_ver | The minimum version of PEBakery required by the script. This is used to ensure compatibility. |
| script_main | An object that contains information about the script as defined in the script's `[Main]` section.

### script_main Object

| Property| Description |
| --- | --- |
| title | The title of the script. |
| desc | The script's description. |
| author | The script's author. |
| version | The script's version. This will be used by the update process to compare with the current script version and determine if an update is required. |

### Example meta.json file

```json
{
  "meta_schema_ver": "0.1",
  "pebakery_min_ver": "0.9.6",
  "script_main": {
    "title": "myScript",
    "desc": "A simple script that does absolutely nothing.",
    "author": "Homes32",
    "version": "1.2"
  }
}
```
