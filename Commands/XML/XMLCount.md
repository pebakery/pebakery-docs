# XMLCount

Count the number of times an `XPath` match is found in an XML file.

## Syntax

```pebakery
XMLCount,<XMLFile>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| XMLFile | Full path to the XML filed to format. |
| DestVar | Variable where the result will be stored. |

## Return Codes

None.

## Remarks

Default namespaces are exposed with the `_` prefix, so you can query the default namespaced XML as:

```
XMLRead,%XmlFile%,//_:SSIDConfig/_:SSID/_:name/text()
```

For more information about using XPath syntax check out this [XPath Tutorial](https://www.w3schools.com/xml/xpath_intro.asp).

## Related

[XMLAdd]], [XMLDelete]], [[XMLRead]], [[XMLUpdate]]

## Examples

### Example 1

#### XML File

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

#### Commands

```pebakery

XMLCount,"C:\Temp\Test.xml","//_:items/_:item",%Count%
// Returns 2
Message,"Items: [%Count%]"

```