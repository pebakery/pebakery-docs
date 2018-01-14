# If,Question

Displays a dialog that asks the user a question, then uses their response to determine if the command should be executed.

## Syntax

```pebakery
If,QUESTION,<Question>,<Command>
```

```pebakery
If,QUESTION,<Question>,<Timeout>,<DefaultAnswer>
```

### Arguments

#### Version 1

| Argument | Description |
| --- | --- |
| Question | The text that will be displayed to the user. |
| Command | The command to be executed if the user choses `Yes`. |

#### Version 2

| Argument | Description |
| --- | --- |
| Question | The text that will be displayed to the user. |
| Command | The command to be executed if the user choses `Yes`. |
| Timeout | Time in seconds before the `DefaultAnswer` is selected. |
| DefaultAnswer | The answer that will be automatically selected after the `Timeout` period expires.
|| Yes<br/>True - The `Command` is executed. |
|| No<br/>False - The `Command` is not executed. |

## Remarks

Questions block further processing until the question is answered. Unless the situation requires user intervention it is recommended to set a reasonable timeout period with a default answer.

## Related

[If](./If.md), [If-Else](./If-Else.md)

## Examples

### Example 1

Ask a question without using a timeout/default answer.

```pebakery
[main]
Title=If-Question Example
Description=Show usage of the If,Question command.
Level=5
Version=1
Author=Homes32

[variables]

[process]
// Run a single command if the user chooses YES
If,QUESTION,"Do you like green eggs and ham?",Message,"You answered YES."

// Run another section if the user chooses YES
If,QUESTION,"Would you like to run another section?",Run,%PluginFile%,Run-Yes

// We can also use Block statements to execute additional commands
// or use an Else condition to perform another action when the user chooses No.
If,QUESTION,"Are you Sure you want to continue?",Begin
  Message,"Processing will continue..."
End
Else,Begin
  Message,"Processing will stop."
  Exit,"User requested stop."
End

[Run-Yes]
Message,"Running another section..."
```

### Example 2

Ask a question and define a 10 second timeout before the default answer is chosen.

```pebakery
[main]
Title=If-Question Example
Description=Show usage of the If,Question command.
Level=5
Version=1
Author=Homes32

[variables]

[process]
// Run a single command if the user chooses YES
// Choose YES as the default answer after 10 seconds
If,QUESTION,"Do you like green eggs and ham?",10,Yes,Message,"You answered YES."

// Run another section if the user chooses YES
// Choose YES as the default answer after 10 seconds
If,QUESTION,"Would you like to run another section?",10,No,Run,%PluginFile%,Run-Yes

// We can also use Block statements to execute additional commands
// or use an Else condition to perform another action when the user chooses No.
// Choose YES as the default answer after 10 seconds
If,QUESTION,"Are you Sure you want to continue?",10,Yes,Begin
  Message,"Processing will continue..."
End
Else,Begin
  Message,"Processing will stop."
  Exit,"User requested stop."
End

[Run-Yes]
Message,"Running another section..."
```