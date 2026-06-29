# XMLQuery

Read XML values.

XMLQuery can return multi-match `XPath` results as a delimited list.

## Syntax

```pebakery
XMLQuery,<XMLFile>,<XPath>,<%DestVar%>[,Text|Xml][,NOERR][,Delim=<Str>]
```

### Arguments

| Argument | Description |
| --- | --- |
| XMLFile | Full path to the XML filed to read. |
| XPath | XPath (XML Path Language) query used to locate the value to read. |
| DestVar | Variable where the value of `XPath` will be stored. |
| Format | **(Optional)** One of the following format options: |
|| `Text` - (Default) Returns the values as a pipe `\|` delimited list. |
|| `XML` - Returns the values as raw XML fragments. |
| NOERR | **(Optional)** Don't Halt if the query fails. (Use if you intend to handle errors yourself).
| Delim= | **(Optional)** Delimiter used to separate the items in the list if multiple filter matches are found. Case Insensitive. **Default:** `\|` |

## Return Codes

| Code | Description |
| --- | --- |
| %^RET% | Returns the of the following:  |
||`0` - Success|
||`1` - XML file missing or invalid.|
||`2` - XPath not found.|

## Remarks

If the `XPath` does not exist the operation will fail and the build will Halt. You can override this behavior by specifying the `NOERR` flag and checking the value of `%^RET%`. If `NOERR` is specified and the `XPath` does not exist `DestVar` will return an empty string.

Default namespaces are exposed with the `_` prefix.

For more information about using XPath syntax check out this [XPath Tutorial](https://www.w3schools.com/xml/xpath_intro.asp).

## Related

[XMLAdd](./XMLAdd.md), [XMLCount](./XMLCount.md), [XMLDelete](./XMLDelete.md), [XMLRead](./XMLRead.md), [XMLReadList](./XMLReadList.md), [XMLRename](./XMLRename.md), [XMLUpdate](./XMLUpdate.md)

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

XMLQuery,"C:\Temp\Test.xml","//_:items/_:item",%Items%
// Returns A|B
Message,"[%Items%]"

```