# Husk design

Pipeline: `scan` (totals per directory) -> `rules.rate` (verdict per candidate) -> `plan.candidates` (outermost only) -> `plan.choose` (budget) -> `apply` (Trash only).

Rating: **SAFE** the owner regenerates it (caches, build output); **PROBABLY_SAFE** recoverable with some cost or a judgement call; **KEEP** not recommended, including everything no rule recognises. Each verdict carries a confidence (0-99), the rule id, a reason and whether it regrows.

Safety: protected folders (Documents, Desktop, Pictures, Movies, Music, Library/Mobile Documents, Mail, Messages, Photos, keychains, ssh keys, system paths) are KEEP unless `--allow-protected`. Apply re-rates each path and refuses any that changed since the plan. No deletion without the Trash.

AI interface: every command has `--json` with `"schema": 1` and a `kind`; exit codes 0/2/3/4; `husk serve` is an MCP server with `husk_scan`, `husk_explain`, `husk_plan`. Apply is not exposed over MCP.

Rejected: deleting with `fs.remove` (no undo); ML scoring (opaque, rules cite reasons); rating every file (noise, slow): only directories and a few file rules are candidates.
