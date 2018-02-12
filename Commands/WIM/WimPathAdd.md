# WimPathAdd

Adds a file or directory tree to a Windows Imaging (.wim) file.

## Syntax

```pebakery
WimPathAdd,<WimFile>,<ImageIndex>,<SrcPath>,<DestPath>[,CHECK][,NOACL][,PRESERVE][,REBUILD]
```

### Arguments

| Argument | Description |
| --- | --- |
| WimFile | The full path of the .wim file to modify. |
| ImageIndex | The index of the image within the .wim file where the files will be added. |
| SrcPath |  The full path of the file or directory to add to the image. |
| DestPath | The full path to the file or directory within the WIM file. If `SrcPath` is a file, `DestPath` must be a file. If `SrcPath` is a directory, `DestPath` must be a directory. All paths are relative to the image's root directory. Any existing duplicate files will be overwritten unless the `PRESERVE` flag is specified. If the directory structure does not exist it will be created. |

### Flags

The following flags can be used independently and can be specified in any order.

| Argument | Description |
| --- | --- |
| CHECK | **(Optional)** Before updating `WimFile`, verify it's integrity if it contains extra integrity information. Also include extra integrity information in the updated WIM even if it was not present before. |
| NOACL | **(Optional)** Do not preserve the security descriptors of files and directories. |
| PRESERVE | **(Optional)** Do not overwrite existing files. |
| REBUILD | **(Optional)** Rebuild the entire WIM instead of appending the data to the end of the image. Rebuilding the WIM is slower, but will recover space that would otherwise be left as a hole in the WIM file. |

## Remarks

**Data integrity:** In order to detect accidental (non-malicious) data corruption, the checksum of every file extracted is calculated and an error is returned if it does not match the checksum included in the WIM file. In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons PEBakery does not verify or create the integrity table by default, but the `CHECK` flag can be specified to make it do so.

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimMount](./WimMount.md), [WimUnmount](./WimUnmount.md), [WimPathDelete](./WimPathDelete.md), [WimPathRename](./WimPathRename.md)

## Examples

### Example 1

This example adds a single file to the 1st image of *C:\Temp\boot.wim*.

```pebakery
Echo,"Adding File..."
WimPathAdd,C:\Temp\boot.wim,1,C:\Windows\regedit.exe,Windows\regedit.exe
```

### Example 2

This example will add the *C:\Temp\Files* directory to the 1st image of *C:\Temp\boot.wim*.

```pebakery
Echo,"Adding Directory..."
WimPathAdd,C:\Temp\boot.wim,1,C:\Temp\Files,"/Program Files/myApp"
```
