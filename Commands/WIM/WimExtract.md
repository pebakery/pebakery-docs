# WimExtract

Extracts one or more files or directory trees from a Windows Imaging (.wim) file.

Wildcards are supported, allowing multiple files or directories to be copied at one time.

Note that `WimExtract` is intended for extracting only a subset of a WIM image. If you want to extract or "apply" a full WIM image use the `WimApply` command instead.

## Syntax

```pebakery
WimExtract,<SrcWim>,<ImageIndex>,<ExtractPath>,<DestDir>[,Split=<String>][,CHECK][,NOACL][,NOATTRIB]
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcWim | The full path of the .wim file to extract files from. |
| ImageIndex | The index of the image within the .wim file containing the files to be extracted. |
| ExtractPath | The full path of the file(s) within the image to be extracted. All paths are relative to the image's root directory. Wildcards (* ?) are allowed. |
| DestDir | The full path to the directory where the files are to be extracted. Any existing duplicate files will be overwritten. If the directory structure does not exist it will be created. |
| Split= | **(Optional)** A string consisting of a shell-style file "GLOB" that specifies the additional parts of the split WIM. The GLOB must expand to include all parts of the split WIM. Wildcards (? *) are supported. |

### Flags

The following flags can be used independently and can be specified in any order.

| Argument | Description |
| --- | --- |
| CHECK | **(Optional)** Verify the integrity of `SrcWim` if it contains extra integrity information. |
| NOACL | **(Optional)** Do not restore security descriptors on extracted files and directories. |
| NOATTRIB | **(Optional)** Do not restore Windows file attributes such as read-only, hidden, etc. |

## Remarks

**Data integrity:** In order to detect accidental (non-malicious) data corruption, the checksum of every file extracted is calculated and an error is returned if it does not match the checksum included in the WIM file. In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons PEBakery does not check the integrity table by default, but the `CHECK` flag can be specified to make it do so.

**ESD files:** PEBakery can extract files from solid-compressed WIMs, or "ESD" (.esd) files, just like from normal WIM (.wim) files. However, Microsoft sometimes distributes ESD files with encrypted segments; PEBakery cannot extract such files until they have been decrypted.

**Split WIMs:** PEBakery supports extracting from split WIM files (.swm) using the `Split=` argument.

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimMount](./WimMount.md), [WimUnmount](./WimUnmount.md), [WimApply](./WimApply.md), [WimExtractBulk](./WimExtractBulk.md)

## Examples

### Example 1

This example extracts a single file from the 1st image of *C:\Temp\boot.wim* to a folder called *C:\Temp\Target*.

```pebakery
Echo,"Extracting Regedit..."
WimExtract,C:\Temp\boot.wim,1,Windows\regedit.exe,C:\Temp\Target
```

### Example 2

This example will extract all .dll files from the *Windows\System32* directory in the 1st image of *C:\Temp\boot.wim* to a folder called *C:\Temp\Target*. Security Descriptors will not be retained.

```pebakery
Echo,"Extracting all dll files from [boot.wim] [Index: 1] to Windows\System32..."
WimExtract,C:\Temp\boot.wim,1,Windows\System32\*.dll,C:\Temp\Target,NOACL
```
