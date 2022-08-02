# Comments

Comments can be used to provide an explanation or annotation in the script in order to make it easier for other developers to understand what your script is doing. They can also be used to "comment out" lines of code while debugging a script.

## Single Line Comments

PEBakery supports the C++ Style `//` single line comments as well as _.ini_ style single line comments using the hash `#` or semicolon `;` delimiters. Each comment must be placed on its own line and begin with a supported comment delimiter. A comment ends when a newline is started.

```pebakery
// This is a comment
# This is also a comment
; This is another comment!
```

## Multi-Line/Block Comments

Block comments are not supported.

## Comment Sections

Section names that begin and end with a hash mark `#` will be treated as a comment section and will be ignored by PEBakery's script engine and syntax checker.

Unlike Single Line Comments, the contents of a Comment Section will not be displayed in the build log.

```pebakery
[#Info#]
This section will be ignored by PEBakery.
```