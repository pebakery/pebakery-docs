# WimDelete

Deletes an image from a Windows Imaging (.wim) file.

`WimDelete` rebuilds the WIM with all unnecessary file data removed. This is different from Microsoft’s ImageX and DISM, which only will delete the directory tree metadata and XML data, leaving the file data intact.

## Syntax

```pebakery
WimDelete,<WimFile>,<ImageIndex>[,CHECK]
```

### Arguments

| Argument | Description |
| --- | --- |
| WimFile | The full path to the .wim file. |
| ImageIndex | The index of the image within the WIM file to delete. |

### Flags

| Argument | Description |
| --- | --- |
| CHECK | **(Optional)** Before deleting an image from the WIM, verify it's integrity if it contains extra integrity information. Also include extra integrity information in the rebuilt WIM, even if it was not present before.  |

## Remarks

It is possible to delete all the images from a WIM and have a WIM with 0 images, although such a file may not be very useful.

**Data integrity:** In order to detect accidental (non-malicious) data corruption, the checksum of every file extracted is calculated and an error is returned if it does not match the checksum included in the WIM file. In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons PEBakery does not verify or create the integrity table by default, but the `CHECK` flag can be specified to make it do so.

**Split WIMs:** PEBakery does not support deleting images from split WIM files (.swm).

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimMount](./WimMount.md), [WimUnmount](./WimUnmount.md), [WimAppend](./WimAppend), [WimInfo](./WimInfo.md), [WimPathDelete](./WimPathDelete.md)

## Examples

### Example 1

In this example we will remove the 1st image (index 1) in a WIM file.

```pebakery
WimDelete,C:\Temp\Boot.wim,1
```