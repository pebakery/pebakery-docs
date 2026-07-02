# JSONFormat

Format and indent a JSON file for easy human reading or compact it for smaller size.

## Syntax

```pebakery
JSONFormat,<JSONFile>[,<Pretty|Compact>][,SortKeys]
```

### Arguments

| Argument | Description |
| --- | --- |
| JSONFile | Full path to the JSON filed to format. |
| Format | **(Optional)** One of the following: |
|| `Compact` - Remove unnecessary line endings, white space and indentation in the JSON file for a smaller file size. |
|| `Pretty` - Format and indent the JSON file for easy human reading. **(Default)**|
| SortKeys | **(Optional)** Sort object keys recursively. |

## Return Codes

None.

## Remarks

Formatting a file that supports JSONC (JSON with comments) will automatically remove all comments and trailing commas during the format process and standardize the file to RFC 8259 compliant JSON.

## Related

[[JSONValidate]]

## Examples

### Example 1

```pebakery

JSONFormat,"C:\Temp\Test.json",Compact

```