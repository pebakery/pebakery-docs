# JSONReadArray

Extract all elements from an array within a JSON file and return them as a delimited string.

## Syntax

```pebakery
JSONReadArray,<JSONFile>,<Path>,<%DestVar%>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| JSONFile | Full path to the JSON filed to read. |
| Path | GJSON or JSONPath notation used to locate the node. | |
| DestVar | Variable where the value of `Path` will be stored. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. Case Insensitive. **Default:** `\|` |

## Return Codes

None.

## Remarks

If the node is not a JSONArray the build will halt.

Additional Info: [Supported JSON addressing schemes](./README.md#json-path-notation)

## Related

[JSONCount](./JSONCount.md), [JSONQuery](./JSONQuery.md), [JSONRead](./JSONRead.md), [JSONType](./JSONType.md)

## Examples

### JSON File

```JSON
{
    "Name": "App",
    "Items": [
        1,
        "two",
        true
    ],
    "Obj": {
        "B": 2,
        "A": 1
    }
}
```

### Example 1

```pebakery

JSONReadKeys,"C:\Temp\Test.json","Obj",%Keys%
// Returns "B|A"
Message,"[%Keys%]"

```

### Example 2

```pebakery

JSONReadKeys,"C:\Temp\Test.json",".",%Keys%
// Returns "Name|Items|Obj"
Message,"[%Keys%]"

```