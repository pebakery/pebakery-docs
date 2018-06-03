# WimExport

Exports an image from a WIM file.

## Syntax

```pebakery
WimExport,<SrcWim>,<ImageIndex>,<DestWim>,[ImageName=<String>],[ImageDesc=<String>],[Split=<String>],[Recomp=<String>],[BOOT],[CHECK|NOCHECK]
```

### Arguments

| Argument | Description |
| --- | --- |
| SrcWim | The full path of the .wim file containing the image to export. |
| ImageIndex | The index of the image to be exported. |
| DestWim | The full path to the .wim file being created. If the WIM file exists it will be rebuilt. The rebuilding process is slower then simply appending the image but will save some space that would otherwise be left as a hole in the WIM. If the directory structure does not exist it will be created. |
| ImageName= | **(Optional)** The unique name for the image being exported. If not specified it will default to the image name used in `SrcWim`. |
| ImageDesc= | **(Optional)** Additional information about the image. If not specified it will default to the description used in `SrcWim`. |
| Split= | **(Optional)** A string consisting of a shell-style file "GLOB" that specifies the additional parts of the split WIM. The GLOB must expand to include all parts of the split WIM. Wildcards (? *) are supported. |
| ReComp= | **(Optional)** Re-compress (optimize) all data in the WIM. This will significantly increase the time needed to optimize the WIM, but it may result in a better compression ratio if the original image was not created using Wimlib. Specify one of the following compression algorithms: |
|| KEEP - Retain the existing compression format. **You must choose this option if `DestWim` already exists.** If you need to change the compression on an existing wim file you can run `WimOptimize` on `DestWim` after exporting. |
|| NONE - No Compression. |
|| XPRESS - Fast compression and decompression, but results in a larger image size. _(Similar to DISM.exe  /compress:fast )_ |
|| LZX - Zip style DEFLATE compression. _(Similar to DISM.exe: /compress:maximum)_ |
|| LZMS - Microsoft's undocumented compression format similar to the LZMA algorithm used by 7zip. Smaller image size, but takes significantly longer to compress. _(Similar to DISM.exe /compress:recovery)_ |

### Flags

| Argument | Description |
| --- | --- |
| BOOT | **(Optional)** Mark the new image as the "bootable" image of the WIM file. |
| CHECK | **(Optional)** Before optimizing the WIM, verify it's integrity if it contains extra integrity information. Also include extra integrity information in the optimized WIM, even if it was not present before.  |
| NOCHECK | **(Optional)** Do not include extra integrity information in the optimized WIM, even if it was present before. |

The `CHECK` and `NOCHECK` flags are mutually exclusive.

## Remarks

**Data deduplication:** The WIM format has built-in deduplication (also called "single instancing") of file contents. Therefore, when an image is exported, only the file contents not already present in the destination WIM will be physically copied. However, a new copy of the image’s metadata resource, which describes the image’s directory structure, will always be created.

**Data integrity:** In order to detect accidental (non-malicious) data corruption, the checksum of every file extracted is calculated and an error is returned if it does not match the checksum included in the WIM file. In addition, a WIM file can include an integrity table (extra checksums) over the raw data of the entire WIM file. For performance reasons PEBakery does not verify or create the integrity table by default, but the `CHECK` flag can be specified to make it do so.

**ESD files:** PEBakery can export images from solid-compressed WIMs, or "ESD" (.esd) files, just like from normal WIM (.wim) files. However, Microsoft sometimes distributes ESD files with encrypted segments; PEBakery cannot export such images until they have been decrypted.

**Split WIMs:** PEBakery supports exporting images from (but not to) split WIM files (.swm) using the `Split=` argument.

This command uses the the open source [Windows Imaging library (wimlib)](https://wimlib.net/).

## Related

[WimAppend](./WimAppend.md), [WimCapture](./WimCapture.md), [WimOptimize](./WimOptimize.md), [WimPathAdd](./WimPathAdd.md), [WimPathDelete](./WimPathDelete.md), [WimPathRename](./WimPathRename.md)

## Examples

### Example 1

Export image 4 from *install.wim* to a new *Install1.wim* file.

```pebakery
WimExport,C:\Temp\Install.wim,4,C:\Temp\Install1.wim
```

### Example 2

Export image 4 from split WIM *install.swm* to an existing *Install2.wim* file and re-compress using the existing compression format.

```pebakery
WimExport,C:\Temp\Install.swm,4,C:\Temp\Install2.wim,ReComp=KEEP,Split="C:\Temp\install*.swm"
```

### Example 3

Export image 4 from *install.wim* to a new *install3.wim* and re-compress using LZMS compression.

```pebakery
WimExport,C:\Temp\Install.wim,4,C:\Temp\Install3.wim,ReComp=LZMS
// Rename to a install.esd
FileRename,C:\Temp\install2.wim,C:\Temp\install3.esd
```