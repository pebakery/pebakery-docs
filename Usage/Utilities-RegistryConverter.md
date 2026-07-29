# Registry Converter

The Registry Converter is a tool in the **Utility** window (`Open Utilities` button on the main window > **Registry Converter** tab) that converts between Windows `.reg` files and PEBakery script registry commands (`RegWrite`, `RegWriteEx`, `RegDelete`), in either direction.

It's designed for two common workflows:

- Converting a `.reg` file exported from `regedit` into ready-to-paste PEBakery script commands.
- Converting `RegWrite`/`RegWriteEx`/`RegDelete` lines from an existing script back into a `.reg` file (**Advanced Users Only**)

## Usage

1. Paste a `.reg` or script text into the **Source** box, or use **Load File...** (drag-and-drop also works from an elevated explorer window).
2. Click **Convert Reg → Script** or **Convert Script → Reg**, depending on the direction you need.
3. The result appears in the **Result** box, with any warnings listed above the output as comments. Use **Copy** or **Save...** to export it, or **Clear** to reset both boxes.

### Hive Prefix

The **Hive Prefix** field (default `Tmp_`) only applies to `.reg → Script` conversion. WinPE builds typically write to an *offline-loaded* hive (via `RegHiveLoad`) rather than the live registry, and an offline-loaded hive is always mounted under `HKLM`. 

e.g. `SOFTWARE` -> `Tmp_Software`

Clear the field to disable this rewrite and keep the original hive/path as-is. This may be necessary if the `.reg` file has already been converted for use with an offline hive.

## Remarks

The converter is conservative: rather than silently producing something that might be wrong, it comments out the affected line(s) and adds a warning explaining why. This happens for:

- **`HKCC` keys** — no fixed offline hive to write to, skipped entirely.
- **`HKU` keys other than `.DEFAULT`** — per-SID user hives have no fixed offline mount point.
- **`CurrentControlSet`** — rewritten to `ControlSet001` since it's a live-kernel alias that doesn't exist in an offline hive.
- **`%Variables%`** — a script variable can't be resolved to a literal value at conversion time, so any entry that appears to contain a variable is commented out with the raw `%Variable%` text preserved for visibility. Note that it is common to see some false-positives if the registry value contains a Windows environment variable such as `%WinDir%` or `%SystemRoot%`. The script converter has no way to tell the difference so it will always err on the side of caution and produce a warning.
- **Registry commands inside `If`/`Else` conditions** (both single-line and `Begin...End` blocks) — extracted and converted, but commented out since the converter can't evaluate the condition to know if the line would actually run.
- **`RegMulti`** — skipped because this command can only modify an existing value in place, so there's no way to reconstruct the resulting full value into a static `.reg` entry.

## Encoding notes

- Legacy `REGEDIT4` `.reg` files are read using the local machine's active ANSI codepage (`.reg` itself has no way to declare one) — double-check output if the source file came from a machine using a different codepage.
- Modern `Windows Registry Editor Version 5.00` `.reg` files are read/written as UTF-16 LE.
- Script output is UTF-8 (no BOM).
