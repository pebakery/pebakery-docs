# WimInfo

Display information about a Windows Imaging (WIM) archive.

## Syntax

```pebakery
WimInfo,<SrcWim>,<ImageIndex>,<Attribute>,<%DestVar%>
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcWim | The full path to the source files to be captured. |
| ImageIndex | The index of the image within the .wim file to retrieve info from. |
|| 0 - Retrieve basic information about the WIM file. See **Basic WIM Attributes** |
|| 1 - Retrieve information about the 1st image in the WIM file. |
|| _n_ - Retrieve information about the _nth_ image in the WIM file. |
| Attribute | The attribute to query. |
| DestVar | The variable where the value of the specified `Attribute` will be stored. |

### Basic WIM Attributes

The following attributes can be retrieved from the WIM file's Header.

| Attribute | Description |
| --- | --- |
| ImageCount | Returns the number of images the WIM file contains. |
| BootIndex | Returns the index of the bootable image in the .wim file. If there are no bootable images available the value will be zero. |
| Compression | Returns the compression used by the WIM file. `NONE` `XPRESS` `LZX` `LZMS`. |

### Image Attributes


| Attribute | Description |
| --- | --- |


## Remarks

Split WIMs: PEBakery does not support retrieving info from split WIM archives (.swm).

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimMount](./WimMount.md), [WimUnmount](./WimUnmount.md), [WimCapture](./WimCapture.md)

## Examples

### Example 1



```pebakery

```
