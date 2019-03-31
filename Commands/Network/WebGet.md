# WebGet

Downloads files from the Internet.

## Syntax

```pebakery
WebGet,<URL>,<DestPath>[,<HashType>=<HashDigest>][,TimeOut=<Int>][,NOERR]
```

### Arguments

| Argument | Description |
| --- | --- |
| URL | URL of the file to download. Supported URI's are `HTTP`, `HTTPS` |
| DestPath | The full path where the downloaded file will be saved. If the path does not exist it will be created. If the file exists it will be overwritten. |
| HashType= | **(Optional)** Hash type to calculate. Supported hash types: `MD5`, `SHA1`, `SHA256`, `SHA384`, `SHA512`. |
| HashDigest | **(Optional)** The Hash digest used to verify the downloaded file. |
| TimeOut= | **(Optional)** The timespan (in seconds) to wait for a response before the request times out. **Default:** 10 |

`HashType=` and `HashDigest` must be used at same time.

### Flags

Flags may be specified in any order.

| Flag | Description |
| --- | --- |
| NOERR | **(Optional)** Do not halt the build if the download fails. It will be the script developer's responsibility to handle the situation gracefully. |

### Return Codes

| Variable | Description |
| --- | --- |
| #r | Contains the HTTP Status code from the most recent WebGet operation. Exceptionally it is set to 0 if a request could not be established (e.g. timeout), and set to 1 if a request succeeded but given hash digest mismatched. When used in conjunction with the NOERR flag the status code can be tested and corrective action is taken when a failure occurs. A list of HTTP Status codes can be found at the [HTTP Status Code Registry](https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml). |

## Remarks

No checks are done to ensure that the local machine has a valid Internet connection or that there is enough disk space to download the file. If required these tests can be made using PEBakery's *Conditional Operators*.

## Related

[Conditional Operators](../Branch/Operators.md), [Variables](./LangRef/Variables.md)

## Examples

### Example 1

```pebakery
// zlib source code will be downloaded to %BaseDir%\zlib.tar.gz.
WebGet,"https://zlib.net/zlib-1.2.11.tar.gz",%BaseDir%\zlib.tar.gz

// Downloaded tar.gz file will be validated with its SHA256 digest.
WebGet,"https://zlib.net/zlib-1.2.11.tar.gz",%BaseDir%\zlib.tar.gz,Hash=SHA256,c3e5e9fdd5004dcb542feda5ee4f0ff0744628baf8ed2dd5d66f8ca1197cb1a1
```

### Example 2

The following script is an example of how we can use WebGet, as well as override its default behavior and only download the file if it does not exist.

```pebakery
[Main]
Title=WebGet Example
Description=Show usage of the WebGet Command
Author=Homes32
Level=5
Version=1

[Variables]
WebGetIfNotExistEx=Run,%ScriptFile%,WebGetIfNotExistEx

[Process]
// Call our macro
WebGetIfNotExistEx,"https://zlib.net/zlib-1.2.11.tar.gz",%BaseDir%\zlib.tar.gz

[WebGetIfNotExistEx]
// Syntax: WebGetIfNotExistEx,<URL>,<DestFile>
Echo,"Checking for #2..."
If,Not,ExistFile,#2,Begin
// File doesn't exist. lets download it!
Echo,"Downloading #2..."
WebGet,#1,#2
End
Else,Begin
// File already exists on disk.
Echo,"#2 already exists! Skipping download."
End
```