# JSONReadKeys

Extract all the property names (keys) from a specific JsonObject within a JSON file and return them as a delimited string.

## Syntax

```pebakery
JSONReadKeys,<JSONFile>,<Path>,<%DestVar%>[,Delim=<Str>]
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

If the node is not a JsonObject the build will halt.

If the element is null, it will be added to the list as an empty string.

If your array contains objects or nested arrays, `DestVar` might end up containing serialized JSON blobs if the array isn't a simple list of strings or numbers.

Additional Info: [Supported JSON addressing schemes](./README.md#JSON Path Notation)

## Related

[JSONCount](./JSONCount.md), [JSONQuery](./JSONQuery.md), [JSONRead](./JSONRead.md), [JSONReadArray](./JSONReadArray.md), [JSONType](./JSONType.md)

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