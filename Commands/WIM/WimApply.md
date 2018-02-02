# WimApply

Extracts ("applies") an image from a Windows Imaging (.wim) file.

Note that `WimApply` is designed to extract, or "apply", entire WIM images. If you want to extract specific files or directories use the `WimExtract` or `WimExtractList` command instead.

## Syntax

```pebakery
WimApply,<SrcWim>,<ImageIndex>,<DestDir>[,CHECK][,NOACL][,NOATTRIB]
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcWim | The full path of the .wim file to be extracted. |
| ImageIndex | The index of the image in the .wim file to be extracted. |
| DestDir | The full path to the directory where the .wim file is to be extracted. Any existing duplicate files will be overwritten. If the directory structure does not exist it will be created. |

### Flags

The following flags can be used independently and can be specified in any order.

| Argument | Description |
| --- | --- |
| CHECK | **(Optional)** Verify the integrity of `SrcWim` if it contains extra integrity information. |
| NOACL | **(Optional)** Do not restore security descriptors on extracted files and directories. |
| NOATTRIB | **(Optional)** Do not restore Windows file attributes such as read-only, hidden, etc. |

## Remarks

Data integrity: In order to detect accidental (non-malicious) data corruption, the checksum of every file extracted is calculated and an error is returned if it does not match the checksum included in the WIM file. In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons PEBakery does not check the integrity table by default, but the `CHECK` flag can be specified to make it do so.

ESD files: PEBakery can extract files from solid-compressed WIMs, or "ESD" (.esd) files, just like from normal WIM (.wim) files. However, Microsoft sometimes distributes ESD files with encrypted segments; PEBakery cannot extract such files until they have been decrypted.

Split WIMs: PEBakery does not support extracting from split WIM files (.swm) at this time.

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimMount](./WimMount.md), [WimUnmount](./WimUnmount.md), [WimExtract](./WimExtract.md), [WimExtractList](./WimExtractList.md)

## Examples

### Example 1

This example will extract (apply) the entire contents of the 1st image from *C:\Temp\boot.wim* to a folder called *C:\Temp\Target*.

```pebakery
WimApply,C:\Temp\boot.wim,1,C:\Temp\Target
```
