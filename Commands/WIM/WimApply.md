# WimApply

Extracts ("applies") an image, or all images, from a Windows Imaging (WIM) archive.

**Warning!** This command is unstable and may be changed in a future release.

## Syntax

```pebakery
WimApply,<SrcWim>,<ImageIndex>,<DestDir>[,CHECK][,NOACL][,NOATTRIB]
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcWim | The full path to the .wim file that to be extracted. |
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

Note that WimApply is designed to extract, or "apply", full WIM images. If you want to extract only certain files or directories from a WIM image, use the `WimExtract` command instead.

Data integrity: WIM files include checksums of file data. To detect accidental (non-malicious) data corruption, wimlib calculates the checksum of every file it extracts and issues an error if it does not have the expected value. (This default behavior seems equivalent to the /verify option of ImageX.) In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons wimlib does not check the integrity table by default, but the `CHECK` flag can be specified to make it do so.

ESD files: wimlib can extract files from solid-compressed WIMs, or "ESD" (.esd) files, just like from normal WIM (.wim) files. However, Microsoft sometimes distributes ESD files with encrypted segments; wimlib cannot extract such files until they are first decrypted.

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimUnmount](./WimUnmount.md)

## Examples

This example will extract (apply) the entire contents of the 1st image from *C:\Temp\boot.wim* to a folder called *C:\Temp\Target*.

### Example 1

```pebakery
WimApply,C:\Temp\boot.wim,1,C:\Temp\Target
```
