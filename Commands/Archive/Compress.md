# Compress

Compress a file or directory into an archive.

**Warning!** This command is unstable and may be changed in a future release.

## Syntax

```pebakery
Compress,<Format>,<SrcPath>,<DestArchive>,[CompressLevel]
```

### Arguments

| Argument | Description |
| --- | --- |
| Format | Archive format: |
|| `7z` - Use the 7-Zip archive format. (Best Compression) |
|| `Zip` - Use the standard Zip format. (Maximum Portability) |
| SrcPath | Full path of the file/directory to compress. |
| DestArchive | Full path where the archive will be created. |
| CompressLevel | **(Optional)** Supported compression levels: |
|| `Store` -  No compression. Best performance for files that don't benefit from compression. |
|| `Fastest` - Fast compression but results in a larger archive size. |
|| `Normal` - **(Default)** Balance between speed and archive size. |
|| `Best` - Maximum compression results in the smallest archive size at the expense of slower compression/decompression. |

## Remarks

All filenames are encoded to UTF-8.

Compression is performed using [7-Zip](https://www.7-Zip.org).

## Related

[Decompress](./Decompress.md)

## Examples

```pebakery
// PEBakery.ini will be compressed into Setting.zip.
Compress,Zip,%BaseDir%\PEBakery.ini,%BaseDir%\Setting.zip
```

```pebakery
// PEBakery.ini will be stored into Setting.7z.
Compress,7z,%BaseDir%\PEBakery.ini,%BaseDir%\Setting.7z,Store
```