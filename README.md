# Husk

A fast disk-space analyzer for macOS written in [AIL](https://github.com/kksimp/ail) (built against ail v0.2.0, see `.ail-version`). It totals every folder, then says what is safe to delete and why. Husk only moves things to the Trash.

```sh
./ail run husk.ail scan --top 15 ~            # biggest folders
./ail run husk.ail explain ~/Library/Caches/Homebrew
./ail run husk.ail plan --max-bytes 20G --out plan.json
./ail run husk.ail apply plan.json            # dry run; --yes to trash
./ail run husk.ail dupes --min-bytes 10M ~/Downloads
./ail run husk.ail serve                      # MCP: husk_scan, husk_explain, husk_plan
```

Agents: add `--json` (schema 1, stable exit codes). See [docs/design.md](docs/design.md). Features still needed in ail: [docs/ail-requests.md](docs/ail-requests.md). Licence: AGPL-3.0.
