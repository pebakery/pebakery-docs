# XMLReadList

Read XML values and return the result as a list.

XMLReadList can return multi-match `XPath` results.

## Syntax

```pebakery
XMLReadList,<XMLFile>,<XPath>,<%DestVar%>[,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| XMLFile | Full path to the XML filed to read. |
| XPath | XPath (XML Path Language) query used to locate the value to read. |
| DestVar | Variable where the value of `XPath` will be stored. |
| Delim= | **(Optional)** Delimiter used to separate the items in the list. Case Insensitive. **Default:** `\|` |

## Return Codes

None.

## Remarks

If the `XPath` does not exist `DestVar` will return an empty string.

Default namespaces are exposed with the `_` prefix.

 - Every element in the XPath must carry the `_:` prefix since they all inherit the default namespace — there's no un-namespaced fallback.
 - Attributes like name and enable don't get the `_:` prefix because attributes don't inherit the default namespace unless explicitly declared.

For more information about using XPath syntax check out this [XPath Tutorial](https://www.w3schools.com/xml/xpath_intro.asp).

## Related

[XMLAdd](./XMLAdd.md), [XMLCount](./XMLCount.md), [XMLDelete](./XMLDelete.md), [XMLQuery](./XMLQuery.md), [XMLRead](./XMLRead.md), [XMLRename](./XMLRename.md), [XMLUpdate](./XMLUpdate.md)

## Examples

### XML File

```XML
<wlan xmlns="urn:test">
	<SSIDConfig>
		<SSID>
			<name>WiFi</name>
		</SSID>
	</SSIDConfig>
	<items>
		<item>A</item>
		<item>B</item>
	</items>
</wlan>
```

### Example 1

```pebakery

XMLReadList,"C:\Temp\TestQuery.xml","//_:items/_:item",%List%,Delim=;
// Returns A;B
Message,"[%List%]"

```