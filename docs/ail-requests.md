# What Husk needs from ail

Husk prototypes on `fs.walk` and `fs.metadata`. These belong in ail, not in Husk (request ADR numbers via the lead thread).

| Need | Why | Husk side, once it lands |
|---|---|---|
| `fs.scan(root)`: one parallel pass giving, per entry, size, **bytes allocated**, mtime, `dev`, `ino`, `nlink`, kind (file, dir, symlink), without following symlinks | `fs.walk` + `fs.metadata` is one stat call per file, follows links, and has no allocation size or inode, so hard links double count and sparse files and APFS clones mislead | fill `alloc`, `dev`, `ino`, `nlink`, `is_symlink` in `scan.scan`; hard-link dedup is already coded |
| `fs.volume(path)`: total, free and purgeable bytes, mount point, filesystem | show free space and warn about other volumes | header line of `scan` |
| `fs.read_range(path, offset, len) bytes ! IoError` | duplicate detection reads head and tail before hashing whole files | pre-filter in `plan.duplicates` |
| `fs.trash(path) str ! IoError`: move to the macOS Trash (NSFileManager `trashItemAtURL`), return the new location | the only safe removal; `Put Back` must work. `fs.remove` and `fs.rename` into `~/.Trash` are workarounds | `plan.trash_item` returns it; the undo manifest records it |
| `fs.walk` that does not follow symlinks (or a documented flag) | cycles and double counting | none |
| `fs.list_dir`/`fs.scan` errors per entry instead of failing the walk | permission-denied folders are normal under `~/Library` | `Scan.errors` |

Until `fs.trash` exists, `husk apply --yes` refuses to remove anything and says so.
