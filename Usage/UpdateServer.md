# Update Server

**Warning: Update functionality is in active development and may change without notice!**

## Update (Meta.json) Schema

As of Schema v0.1.1 the following meta-data fields are supported in the meta.json file.

### Main Object

| Property| Description |
| --- | --- |
| meta_schema_ver | The version of the schema used for this meta.json file. PEBakery uses this information to determine which data values are supported. |
| pebakery_min_ver | The minimum version of PEBakery required by the script. This is used to ensure compatibility. |
| created_at | Timestamp of when the current meta.json file was created. |
| index | This object contains information about the folder, script, or file to be updated. |
| kind | The type of update. |
|| Folder - A folder. |
|| Script - A script. |
|| NonScriptFile - Other file (ie. an executable or text file) |
| name | The name of the file or folder being updated. |
| file_metadata | This object contains information about a file. |
| script_info | This object contains information about a script. |

### file_metadata object

| Property| Description |
| --- | --- |
| updated_at | Timestamp indicating when the script was last modified. |
| file_size | The script's file size in bytes. |
| sha256 | SHA256 Hash of the script. Used to verify the script's integrity during an update. |

### script_info Object

| Property| Description |
| --- | --- |
| format | The file format of the script. Must be one of the following: |
|| ini_based - Classic Winbuilder `.script` format. |

### ini_based object

If the script_info objects `format` property is set to `ini_based` this object contains information about the script as defined in the script's `[Main]` section.

| Property| Description |
| --- | --- |
| title | The title of the script. |
| desc | The script's description. |
| author | The script's author. |
| version | The script's version. This will be used by the update process to compare with the current script version and determine if an update is required. |

### Example meta.json file

Meta file *myScript.meta.json* for the script *myScript.script*.


```json
{
  "schema_ver": "0.1.1",
  "pebakery_min_ver": "0.9.6",
  "created_at": "2019-10-03T14:15:33.3429239Z",
  "index": {
    "kind": "script",
    "name": "myScript.script",
    "file_metadata": {
      "updated_at": "2019-10-03T13:55:05.8257554Z",
      "file_size": 63969,
      "sha256": "EPfzGPO6B9jQRNGrymK9GO6iluW87/2AAjL8hQWsOp4="
    },
    "script_info": {
      "format": "ini_based",
      "ini_based": {
        "title": "Test Script",
        "desc": "Used for testing PEBakery's updater.",
        "author": "Homes32",
        "version": "1.0.0.0"
      }
    }
  }
}
```
