# JSONQuery

Read values from a JSON file.

JSONQuery can return multi-match filter results as a delimited list.

## Syntax

```pebakery
JSONQuery,<JSONFile>,<Filter>,<%DestVar%>[,Raw|Json|Compact][,NOERR][,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| JSONFile | Full path to the JSON filed to read. |
| Filter | JSON filter used to locate the value(s) to read. |
| DestVar | Variable where the value of `Path` will be stored. |
| Format | **(Optional)** One of the following format options: |
|| `Raw` - **(Default)** Returns the values as a pipe `\|` delimited list. |
|| `Json` - Returns the values as a JSON array. |
|| `Compact` - Returns the values as a compact JSON array. |
| NOERR | **(Optional)** Don't Halt if the query fails. (Use if you intend to handle errors yourself).
| Delim= | **(Optional)** Delimiter used to separate the items in the list if multiple filter matches are found. Case Insensitive. **Default:** `\|` |

## Return Codes

| Code | Description |
| --- | --- |
| %^RET% | Returns the of the following:  |
||`0` - Success|
||`1` - JSON file missing or invalid.|
||`2` - No matches for `Filter` were found.|

## Remarks

If the `Filter` does not find at least one match the operation will fail and the build will Halt. You can override this behavior by specifying the `NOERR` flag and checking the value of `%^RET%`. If `NOERR` is specified and the `Filter` does not exist `DestVar` will return an empty string.

When using `Raw` formatting, if your `Filter` resolves to a node that is not a simple field value (bool/number/string), `DestVar` will return a serialized JSON blob containing the entire object or array.

Additional Info: [Supported JSON addressing schemes](./README.md#JSON Path Notation)

## Related

[JSONCount](./JSONCount.md), [JSONRead](./JSONRead.md), [JSONReadArray](./JSONReadArray.md), [JSONReadKeys](./JSONReadKeys.md), [JSONType](./JSONType.md)

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

JSONQuery,"C:\Temp\Test.json","Obj.A",%Value%
// Returns "1"
Message,"[%Value%]"

```

### Example 2

```pebakery

JSONQuery,"C:\Temp\Test.json","Name2",%Value%,NOERR
If,Not,%^RET%,Equal,0,Set,%Value%,"foo"
// Returns "foo"
Message,Return [%Value%]

```

### Another JSON File

```JSON
{
    "Name": "MyApp",
    "Version": "1.0.0",
    "Build": 42
}
```

### Example 3

This query retrieves multiple results using a comma separated filter. Matches are returned in the order the are specified in the filter.

```pebakery

JSONQuery,"C:\Temp\AnotherTest.json","Name,Build,Version",%Value%
// Returns "MyApp|42|1.0.0"
Message,"[%Value%]"

```

### Example 4

This query retrieves multiple results using a comma separated filter. Missing keys (no match) are ignored.

```pebakery

JSONQuery,"C:\Temp\AnotherTest.json","Name,Missing",%Value%
// Returns "MyApp"
Message,"[%Value%]"

```

### Yet Another JSON File

```JSON
{
    "Name": "App",
    "Items": [
        {
            "Name": "Alice"
        },
        {
            "Name": "Bob"
        }
    ]
}
```

### Example 5

Multi-path filter can mix flat properties with wildcard sub-paths.

```pebakery

JSONQuery,"C:\Temp\YetAnotherTest.json","Name,Items[*].Name",%Value%
// Returns "App|Alice|Bob"
Message,"[%Value%]"

```

