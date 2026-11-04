# AGENTS.md — Husk

Husk finds what is using disk space on macOS and rates each item SAFE, PROBABLY_SAFE or KEEP.
It is written 100% in AIL (https://github.com/kksimp/ail); the toolchain is the `ail` CLI pinned in `.ail-version`.

- Builds and tests run on the designer's machines (Mac, ail-linux, ail-win), never in a cloud container. Run `tools/check.sh` there (check, fmt, tests).
- A missing language or std feature goes into ail, not around it: add it to `docs/ail-requests.md` and tell the ail lead. ADR numbers come from the lead thread.
- Husk never deletes. The only removal route is `plan.trash_item` (the Trash, with an undo manifest). Never call `fs.remove`.
- Rules are data (`rules/rules.ail`, `builtin()`). Add a rule plus a `@test`; never special-case a path in code.
- `model`, `scan`, `rules` and `plan` are the library the GUI uses. They must not print or read stdin; `husk.ail` is the CLI.
- App code never merges into the ail repository.
