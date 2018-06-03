# Compress

Compress a file or directory into archive.

**Warning!** This command is unstable and may be changed in a future release.

## Syntax

```pebakery
Compress,<Format>,<SrcPath>,<DestArchive>,[CompressLevel],[Encoding]
```

### Arguments

| Argument | Description |
| --- | --- |
| Format | Archive format. Only `Zip` is supported at this time. |
| SrcPath | Full path of the file/directory to compress. |
| DestArchive | Full path where the archive will be created. |
| CompressLevel | **(Optional)** This effects archive size and compression time. Supported compression: `Store`, `Fastest`, `Normal`, `Best`. **Default** is `Normal`. |
| Encoding | **(Optional)** Encoding to be used in filename. Supported options: `UTF8`, `UTF16`, `UTF16BE`, `ANSI`. **Default** is `UTF8`. |

`CompressLevel` and `Encoding` can be used independently.

## Remarks

This command depends on [SharpCompress](https://github.com/adamhathcock/sharpcompress)

## Related

[Decompress](./Decompress.md)

## Examples

```pebakery
// PEBakery.ini will be compressed into Setting.zip.
Compress,Zip,%BaseDir%\PEBakery.ini,%BaseDir%\Setting.zip
```

```pebakery
// PEBakery.ini will be stored into Setting.zip.
Compress,Zip,%BaseDir%\PEBakery.ini,%BaseDir%\Setting.zip,Store
```