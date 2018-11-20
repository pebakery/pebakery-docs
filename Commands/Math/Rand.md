# Math,Rand

Generates a pseudo-random positive integer.

## Syntax

```pebakery
Math,Rand,<%DestVar%>[,<Min>,<Max>]
```

### Arguments

| Argument | Description |
| --- | --- |
| DestVar | The variable where the result will be stored. |
| Min | **(Optional)** A positive integer representing the minimum range. (Default is 0) |
| Max | **(Optional)** A positive integer representing the maximum range. (Default is 65536) |

If you choose to define a range you must specify both `Min` and `Max` values.

## Remarks

This command is not designed to be cryptographically secure.

## Related

## Examples

### Example 1

The following script will generate between 1 to 10 pseudo-random numbers.

```pebakery
[Main]
Title=Math-Rand Example
Description=Show usage of the Math,Rand Command
Author=Homes32
Level=5

[Variables]

[Process]
Math,Rand,%i%,1,10
Loop,%ScriptFile%,getRandomNum,1,%i%
Message,"Generated [%i%] pseudo-random numbers:#$x#$x%numList%"

[getRandomNum]
Math,Rand,%randomNumber%
List,Append,%numList%,%randomNumber%
```