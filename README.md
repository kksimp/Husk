# Husk

Husk finds what is taking up disk space on your Mac and tells you what is safe to delete, and why. It is written entirely in [AIL](https://github.com/kksimp/ail).

- **Fast:** one bulk scan (`fs.scan`), parallel across folders.
- **Smart:** every item is rated SAFE, PROBABLY SAFE or KEEP with a plain reason.
- **Safe:** deletes only go to the Trash (`fs.trash`), and every apply writes an undo manifest.
- **AI-first:** `husk scan --json`, `husk explain PATH`, `husk plan`, `husk apply`.

Status: early development. Pinned AIL commit goes in `.ail-version`.

License: AGPL-3.0 (see `LICENSE`). Private repository.
