# JSONWrite

Add/Modify values in a JSON file.

## Syntax

```pebakery
JSONWrite,<JSONFile>,<Path>,<Value>
```

### Arguments

| Argument | Description |
| --- | --- |
| JSONFile | Full path to the JSON file to read. |
| Path | SJSON or JSONPath notation used to locate the value to write. |
| Value | The value to write. |

## Return Codes

None.

## Remarks

When using JSONPath the path/value will only be written when it matches exactly one existing node. In order to add a value that does not exist you must use SJSON notation.

When modifying files that support JSONC (JSON with comments), the system will automatically remove all comments and trailing commas during the write process and standardize the file to RFC 8259 compliant JSON.

Additional Info: [Supported JSON addressing schemes](./README.md#JSON Path Notation)

## Related

[JSONCount](./JSONCount.md), [JSONDelete](./JSONDelete.md), [JSONQuery](./JSONQuery.md), [JSONRead](./JSONRead.md), [JSONReadArray](./JSONReadArray.md), [JSONReadKeys](./JSONReadKeys.md), [JSONType](./JSONType.md)

## Examples

### JSON File

```JSON
{
    "JS_TASKBAR": {
        "theme": "light"
    },
    "Microsoft.PowerShell:ExecutionPolicy": "RemoteSigned",
    "Items": [
        1,
        "two"
    ]
}
```

### Example 1

Add an non-existing value to a JSON file (GJSON).

```pebakery

JSONWrite,"C:\Temp\Test.json","JS_FILEEXPLORER.4th_filename","explorer++.exe"

```

### Example 2

Update an existing value (JSONPath).

```pebakery

// Change JS_TASKBAR theme from light to dark
JSONWrite,"C:\Temp\Test.json","$.JS_TASKBAR.theme","dark"

```