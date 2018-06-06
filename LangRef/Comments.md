# Comments

Comments can be used to provide an explanation or annotation in the script in order to make it easier for other developers to understand what your script is doing. They can also be used to "comment out" lines of code while debugging a script. PEBakery supports both single and multi-line comments.

## Single Line Comments

PEBakery supports the C++ Style `//` single line comments as well as _.ini_ style single line comments using the hash `#` or semicolon `;` delimiters. Each comment must be placed on its own line and begin with a supported comment delimiter. A comment ends when a newline is started.

```pebakery
// This is a comment
# This is also a comment
; This is another comment!
```

Single line comments can also be used to comment out block comments.

```pebakery
// /*
Echo,"This code will be executed..."
// */
```

## Multi-Line/Block Comments

Block comments are defined by the C Style `/* */` character sequence and can span multiple lines of code. A comment begins with the `/*` sequence and must end with the `*/` sequence. Everything in between is regarded as a comment.

```pebakery
/* Block comment used as a single line comment */

/* Echo,"This code never gets to run"
Echo,"This code will not run either" */

/*
Echo,"This code never gets to run"
Echo,"This code will not run either"
*/
```

**Note:** Comment end `*/` must always be placed at the end of a line.

```pebakery
// Correct
/*
Echo,"Hello World!"
*/
Echo,"Goodbye World!"
```

```pebakery
// Incorrect (Syntax Error)
/*
Echo,"Hello World!"
*/ Echo,"Goodbye World!"
```