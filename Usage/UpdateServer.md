# Update Server

**Warning: Update functionality is in active development and may change without notice!**

## Update (Meta.json) Schema

As of Schema v0.1 the following meta-data fields are supported in the meta.json file.

### Main Object

| Property| Description |
| --- | --- |
| meta_schema_ver | The version of the schema used for this meta.json file. PEBakery uses this information to determine which data values are supported. |
| pebakery_min_ver | The minimum version of PEBakery required by the script. This is used to ensure compatibility. |
| hash_sha256 | SHA256 Hash of the script. Used to verify the script's integrity during an update. |
| last_write | Timestamp indicating the last update of the current meta.json file. |
| file_size | The script's file size in bytes. |
| script_format | The file format of the script. Must be one of the following: |
|| Winbuilder - Classic Winbuilder `.script` format. |
| wb_script_info | If the `script_format` is `Winbuilder` this object contains information about the script as defined in the script's `[Main]` section. |

### wb_script_info Object

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
   "meta_schema_ver": "0.1",
    "pebakery_min_ver": "0.9.6",
    "hash_sha256": "ObyT2vDKEsNzvEPNCrd7TTwXtmsYvbxXr3kKY4obXsE=",
    "last_write": "2019-08-16T20:13:47.2649463Z",
    "file_size": 1093,
    "script_format": "Winbuilder",
    "wb_script_info": {
        "title": "My Script",
        "desc": "A simple test script.",
        "author": "ied206",
        "version": "1.2"
    }
}
```
