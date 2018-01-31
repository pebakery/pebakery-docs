# WimExtract

Extracts one or more files or directory trees from a Windows Imaging (WIM) archive.

Wildcards are supported, allowing multiple files or directories to be copied at one time.

**Warning!** This command is unstable and may be changed in a future release.

## Syntax

```pebakery
WimExtract,<SrcWim>,<ImageIndex>,<DestDir>,<ExtractPath>,[CHECK],[NOACL],[NOATTRIB]
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcWim | The full path of the .wim file to extract files from. |
| ImageIndex | The index of the image within the .wim file containing the files to be extracted. |
| DestDir | The full path to the directory where the files are to be extracted. Any existing duplicate files will be overwritten. If the directory structure does not exist it will be created. |
| ExtractPath | The full path of the file(s) within the image to be extracted. Wildcards (*, ?) are allowed. |

### Flags

The following flags can be used independently and can be specified in any order.

| Argument | Description |
| --- | --- |
| CHECK | **(Optional)** Verify the integrity of `SrcWim` if it contains extra integrity information. |
| NOACL | **(Optional)** Do not restore security descriptors on extracted files and directories. |
| NOATTRIB | **(Optional)** Do not restore Windows file attributes such as read-only, hidden, etc. |

## Remarks

Note that `WimExtract` is intended for extracting only a subset of a WIM image. If you want to extract or "apply" a full WIM image use the `WimApply` command instead.

Data integrity: WIM files include checksums of file data. To detect accidental (non-malicious) data corruption, wimlib calculates the checksum of every file it extracts and issues an error if it does not have the expected value. (This default behavior seems equivalent to the /verify option of ImageX.) In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons wimlib does not check the integrity table by default, but the `CHECK` flag can be specified to make it do so.

ESD files: wimlib can extract files from solid-compressed WIMs, or "ESD" (.esd) files, just like from normal WIM (.wim) files. However, Microsoft sometimes distributes ESD files with encrypted segments; wimlib cannot extract such files until they are first decrypted.

The `WimExtract` command supports extracting files and directory trees from stand-alone WIMs as well as split WIMs

**This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).**

## Related

[WimUnmount](./WimUnmount.md)

## Examples

This example will extract (apply) the entire contents of the 1st image from *C:\Temp\boot.wim* to a folder called *C:\Temp\Target*.

### Example 1

```pebakery
WimApply,C:\Temp\boot.wim,1,C:\Temp\Target
```
