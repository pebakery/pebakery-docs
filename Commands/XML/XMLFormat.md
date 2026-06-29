# XMLFormat

Format and indent an XML file for easy human reading or compact it for smaller size.

## Syntax

```pebakery
XMLFormat,<XMLFile>[,Pretty|Compact]
```

### Arguments

| Argument | Description |
| --- | --- |
| XMLFile | Full path to the XML filed to format. |
| Format | **(Optional)** One of the following: |
|| `Pretty` - **(Default)** Format and indent the XML file for easy human reading. |
|| `Compact` - Remove unnecessary line endings, white space and indentation in the XML for a smaller file size. |

## Return Codes

None.

## Remarks

None.

## Related

[XMLAdd](./XMLAdd.md), [XMLDelete](./XMLDelete.md), [XMLRead](./XMLRead.md), [XMLValidate](./XMLValidate.md), [XMLUpdate](./XMLUpdate.md)

## Examples

### Example 1

```pebakery

XMLFormat,"C:\Temp\Test.xml",Pretty

```