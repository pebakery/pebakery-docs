# XMLDelete

Delete an XML path/value.

## Syntax

```pebakery
XMLDelete,<XMLFile>,<XPath>
```

### Arguments

| Argument | Description |
| --- | --- |
| XMLFile | Full path to the .xml filed to edit. |
| XPath | XPath (XML Path Language) query used to locate the Attribute/Element to delete. |

## Return Codes

None.

## Remarks

If the command fails the build will halt.

Default namespaces are exposed with the `_` prefix.

 - Every element in the XPath must carry the `_:` prefix since they all inherit the default namespace — there's no un-namespaced fallback.
 - Attributes like name and enable don't get the `_:` prefix because attributes don't inherit the default namespace unless explicitly declared.

For more information about using XPath syntax check out this [XPath Tutorial](https://www.w3schools.com/xml/xpath_intro.asp).

## Related

[[XMLAdd]], [[XMLRename]], [[XMLUpdate]]

## Examples

### Example 1

```pebakery

// Delete a Subnode called GUIConfig under NotepadPlus
XMLDelete,%config.xml%,"NotepadPlus/GUIConfigs"

```