# Log Settings

Settings related to PEBakery's log handling.

PEBakery stores all system and build logs in a SQLLite database.

## Settings

Log settings may be configured via the **PEBakery > Settings > Log** tab or by manually editing `PEBakery.ini` located in PEBakery's root directory *(eg. C:\PEBakery\PEBakery.ini)*.

### Logging

| Setting | Default | Description |
| --- | --- | --- |
| Clear Logs | | Pressing this button will clear the log database. |
| Debug Level | Production | This setting can be adjusted to provide more detailed debug logging. |
| | Production | Normal logging. |
| | PrintException | Include runtime exceptions in the log. |
| | PrintExceptionStackTrace | Include runtime exceptions and a full stack trace in the log. |

### Optimization

| Setting | Default | Description |
| --- | --- | --- |
| Deferred Logging | True | This setting dramatically increases performance by deferring log writes to the database until after the script execution has completed. **Disabling this setting is not recommended.** |
| Compact exported HTML log | True | Enable compacting the HTML logs to save space. |