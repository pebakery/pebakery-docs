# WimOptimize

Rebuilds a Windows Imaging (.wim) file.

The new WIM is written to a temporary file, and renamed to the original filename once the rebuild is complete. Rebuilding will remove any holes that have been left in the WIM as a result of appending or deleting files or images, so the new WIM may be smaller than the old WIM.

By default, `WimOptimize` will reuse existing compressed data however, it is also possible to re-compress the WIM file using another algorithm during the rebuild process.

## Syntax

```pebakery
WimOptimize,<WimFile>[,RECOMPRESS[=<STR>]][,CHECK|NOCHECK]
```

### Arguments

| Argument | Description |
| --- | --- |
| WimFile | The full path of the .wim file to optimize. |
| RECOMPRESS= | **(Optional)** Re-compress all data in the WIM. This will significantly increase the time needed to optimize the WIM, but it may result in a better compression ratio if the original image was not created using Wimlib. To rebuild the WIM with the existing compression format use `RECOMPRESS`. To change the compression algorithm use `RECOMPRESS=` and specify one of the following compression algorithms: |
|| NONE - No Compression. |
|| XPRESS - Fast compression and decompression, but results in a larger image size. _(Similar to DISM.exe  /compress:fast )_ |
|| LZX - Zip style DEFLATE compression. _(Similar to DISM.exe: /compress:maximum)_ |
|| LZMS - Microsoft's undocumented compression format similar to the LZMA algorithm used by 7zip. Smaller image size, but takes significantly longer to compress. _(Similar to DISM.exe /compress:recovery)_ |

### Flags

The following flags are mutually exclusive.

| Argument | Description |
| --- | --- |
| CHECK | **(Optional)** Before optimizing the WIM, verify it's integrity if it contains extra integrity information. Also include extra integrity information in the optimized WIM, even if it was not present before.  |
| NOCHECK | **(Optional)** Do not include extra integrity information in the optimized WIM, even if it was present before. |

## Remarks

**Data integrity:** In order to detect accidental (non-malicious) data corruption, the checksum of every file extracted is calculated and an error is returned if it does not match the checksum included in the WIM file. In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons PEBakery does not verify or create the integrity table by default, but the `CHECK` flag can be specified to make it do so.

**Split WIMs:** `WimOptimize` does not support split WIMs or delta WIMs.

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimAppend](./WimAppend.md), [WimCapture](./WimCapture.md), [WimPathAdd](./WimPathAdd.md), [WimPathDelete](./WimPathDelete.md), [WimPathRename](./WimPathRename.md)

## Examples

### Example 1

Rebuild *install.wim*.

```pebakery
WimOptimize,C:\Temp\Install.wim
```

### Example 2

Rebuild and re-compress *install.wim*.

```pebakery
WimOptimize,C:\Temp\Install.wim,RECOMPRESS
```

### Example 3

Rebuild and re-compress *install.wim* using LZX compression.

```pebakery
WimOptimize,C:\Temp\Install.wim,RECOMPRESS=LXZ
// Rename to a install.esd
FileRename,C:\Temp\install.wim,C:\Temp\install.esd
```