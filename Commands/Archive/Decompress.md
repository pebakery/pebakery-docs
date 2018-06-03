# Decompress

Extract files from a archive.

**Warning!** This command is unstable and may be changed in a future release.

## Syntax

```pebakery
Decompress,<FileName>,<DestDir>,[Encoding]
```

### Arguments

| Argument | Description |
| --- | --- |
| FileName | Full path of the archive to extract. |
| DestDir | Full path to the directory where the archive will be extracted. |
| Encoding | **(Optional)** Encoding used in the filename. Supported types are: `UTF8`, `UTF16`, `UTF16BE`, `ANSI`. |

## Supported Archive Formats

If the `Encoding` argument is not specified, *SevenZipExtractor* will be used in order to achieve maximum performance. Otherwise *SharpCompress* will be used.

| Mode | Supported Archive Formats |
| --- | --- |
| Native (7z.dll) | 7z, APM, AR, ARJ, BZIP2, CAB, CHM, CPIO, CramFS, DEB, DMG, EXT, FAT, GPT, GZIP, HFS, IHEX, ISO, LZH, LZMA, MBR, MSI, NSIS, NTFS, QCOW2, RAR, RPM, SquashFS, TAR, UDF, UEFI, VDI, VHD, VMDK, WIM, XAR, XZ, Z, ZIP |
| Managed (SharpCompress.dll) | 7z, BZIP2, CAB, GZIP, RAR (RAR5 is **not** supported), TAR, ZIP |

## Remarks

This command depends on [SharpCompress](https://github.com/adamhathcock/sharpcompress) (Managed) or [SevenZipExtractor](https://github.com/adoconnection/SevenZipExtractor) and `7z.dll` (Native).

## Related

[Compress](./Compress.md)

## Example

```pebakery
// Setting.7z will be extracted to %DestDir%.
Decompress,%SrcDir%\Setting.7z,%DestDir%
```
