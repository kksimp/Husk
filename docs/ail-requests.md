# What Husk needs from ail

All landed in ail 09cfac57: `fs.scan` (ADR 0927), `fs.volume` (0928), `fs.read_range` and `fs.trash` (0929). Husk uses them. Remaining wishes: `fs.trash` returning the new location for the undo manifest, and per-device byte totals.

`fs.scan_count` (ADR 0992, ail #1088) drives the live progress bar: a ticker task reads it every 150 ms while a root is scanned. Needs a pin that includes #1088.
