# WimExtractBulk

Uses a "list file" to extract one or more files or directory trees from a Windows Imaging (.wim) file.

Wildcards are supported, allowing multiple files or directories to be copied at one time.

Note that `WimExtractBulk` is intended for extracting only a subset of a WIM image. If you want to extract or "apply" a full WIM image use the `WimApply` command instead.

## Syntax

```pebakery
WimExtractBulk,<SrcWim>,<ImageIndex>,<ListFile>,<DestDir>[,Split=<String>][,CHECK][,NOACL][,NOATTRIB][,NOERR][,NOWARN]
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcWim | The full path of the .wim file to extract files from. |
| ImageIndex | The index of the image within the .wim file containing the files to be extracted. |
| ListFile | The full path a text file that contains a list of paths to extract. See the _List File Specification_ below for more details. |
| DestDir | The full path to the directory where the files are to be extracted. Any existing duplicate files will be overwritten. If the directory structure does not exist it will be created. |
| Split= | **(Optional)** A string consisting of a shell-style file "GLOB" that specifies the additional parts of the split WIM. The GLOB must expand to include all parts of the split WIM. Wildcards (? *) are supported. |

### Flags

The following flags can be used independently and can be specified in any order.

| Argument | Description |
| --- | --- |
| CHECK | **(Optional)** Verify the integrity of `SrcWim` if it contains extra integrity information. |
| NOACL | **(Optional)** Do not restore security descriptors on extracted files and directories. |
| NOATTRIB | **(Optional)** Do not restore Windows file attributes such as read-only, hidden, etc. |
| NOERR | **(Optional)** Do not fail if a path or GLOB does not exist in the `SrcWim`. A warning will be logged for the failed match and processing will continue with the next path. |
| NOWARN | **(Optional)** Do not log a warning if a path or GLOB does not exist in the `SrcWim`. A message will still be generated in the log, however it will have a `Muted` state. |

### List File Specification

List files are text files that contain a list of paths to extract from the WIM image.

List files must must obey the following rules:

- Only one path is allowed per line.
- All paths are relative to the image's root directory.
- Paths are not case sensitive.
- Wildcards (*, ?) are allowed and may expand to include multiple files or directories.
- Both fowardslash `/` and backslash `\` characters are supported. The leading `\` is optional.
- Comments must be on their own line and begin with `;` or `#`.
- It's not necessary to quote paths containing spaces. (ex. _\Program Files\Common Files_)
- Whitespace is ignored.

Note: PEBakey internally converts the list file to use `UTF-16LE` encoding.

#### List File Example

```pebakery
; This is a comment
# This is also a comment
\Users
\Windows\explorer.exe
Windows\System32\en-US\*

; It’s not necessary to quote paths containing internal spaces.
/Program Files/M*

; Leading and trailing whitespace is ignored

   \Windows\notepad*

```

## Remarks

**Data integrity:** In order to detect accidental (non-malicious) data corruption, the checksum of every file extracted is calculated and an error is returned if it does not match the checksum included in the WIM file. In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons PEBakery does not check the integrity table by default, but the `CHECK` flag can be specified to make it do so.

**ESD files:** PEBakery can extract files from solid-compressed WIMs, or "ESD" (.esd) files, just like from normal WIM (.wim) files. However, Microsoft sometimes distributes ESD files with encrypted segments; PEBakery cannot extract such files until they have been decrypted.

**Split WIMs:** PEBakery supports extracting from split WIM files (.swm) using the `Split=` argument.

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimMount](./WimMount.md), [WimUnmount](./WimUnmount.md), [WimApply](./WimApply.md), [WimExtract](./WimExtract.md)

## Examples

### Example 1

This example extracts multiple files and directories from the 4th image of *C:\Temp\install.wim* to a folder called *C:\Temp\Target* using a `ListFile` called *FileList.txt*.

```pebakery
Echo,"Extracting from ListFile..."
WimExtractBulk,%install.wim%,4,C:\Temp\Target\FileList.txt,C:\Temp\Target\Extract,NOACL
```

FileList.txt

```pebakery
; Directories
Windows\Fonts\
Program Files\
Windows\Globalization\
Windows\??-??\
Windows\system32\en-US\
Program Files\
ProgramData\
users\
Windows\inf\
Windows\winsxs\*_microsoft-windows-servicingstack*\
Windows\servicing\
Windows\system32\boot\
Windows\system32\Dism\
Windows\system32\driverstore\
Windows\system32\drivers\
Windows\system32\wbem\
Windows\system32\Recovery\
Windows\system32\SMI\

Windows\winsxs\*_microsoft.windows.c..-controls.resources*\
Windows\winsxs\*_microsoft.windows.common-controls*\
Windows\winsxs\*_microsoft.windows.gdiplus*\
Windows\winsxs\*_microsoft.windows.isolationautomation*\
Windows\Globalization\

; Files
Windows\*.*

Windows\Boot\PXE\??-??\bootmgr.exe.mui
Windows\Boot\EFI\bootmgfw.efi
Windows\system32\config\components
Windows\system32\config\Default
Windows\system32\config\sam
Windows\system32\config\Security
Windows\system32\config\software
Windows\system32\config\system
Windows\winsxs\manifests\*_microsoft.windows.c..-controls.resources*
Windows\winsxs\manifests\*_microsoft.windows.common-controls*
Windows\winsxs\manifests\*_microsoft.windows.gdiplus*
Windows\winsxs\manifests\*_microsoft.windows.isolationautomation*
Windows\winsxs\manifests\*_microsoft.windows.systemcompatible*
Windows\winsxs\manifests\*_microsoft.windows.i..utomation.proxystub*
Windows\system32\api-ms-*.dll
Windows\system32\*.dat
Windows\system32\*.exe
Windows\system32\??-??\*.exe.mui
Windows\system32\??-??\*.ocx.mui
Windows\WindowsShell.Manifest
Windows\system32\*.ocx
Windows\system32\*.com
Windows\system32\*.cmd
Windows\system32\hal*.dll
Windows\system32\KBDUS.DLL
Windows\system32\KBD*.DLL
```
