# Husk GUI

One `std.app` canvas (`husk.ail gui`, `view/view.ail`), Safari-style dark like Garlic.

- **Sidebar:** volume usage bar (green slice = what the current selection would free), Overview, Safe to delete, categories with sizes.
- **Toolbar:** clickable breadcrumb; scan progress bar while `pct < 1` (fed by `external` events `scan` with `pct|files|path`), else Rescan.
- **Treemap** (`treemap/`, squarified, tested): tiles colored green / amber / red by safety; click selects, click a selected folder drills in.
- **List:** sortable Name / Size / Safety, size bars, safety badge, reason, tick boxes; scrolls.
- **Detail band:** reason, size, last used, full path of the selected item.
- **Footer + sheet:** "Select all safe", "Review & Move to Trash…" opens a sheet listing exactly what goes; Undo after.
- **Keys:** Backspace goes up, Escape closes the sheet.

`mock/` is a MOCK tree. The core lane's model replaces it; the GUI needs `Entry{name,size,is_dir,safety,reason,cat,parent,kids,age}`.

## Needed in ail (not worked around)

1. `fs.trash` (the sheet's Move to Trash only hides entries now), `fs.scan` progress events, `fs.volume`.
2. Landed and used: hover `move`/`leave` (std.app.16), `clicks` (std.app.17), popup menus (std.app.18), `Shade` (std.app.19), clipboard (std.app.26). Still to adopt: host text measuring (std.app.13) in place of `look.width`.

Not built or run yet: builds happen on Kaleb's machines.

## Scanning (2026-11-06)

The window opens on a welcome page (nothing scanned yet): Smart scan, Home, Xcode and simulators, Library, Whole disk, each a card and a sidebar entry; a folder field plus Scan button above the canvas (Return also scans); `husk.ail gui PATH` scans at once. A scan task takes requests from a channel, so Rescan and the sidebar entries work any time. Several roots (Smart scan) merge under a top entry "This Mac".

macOS cleanup rules (rules/rules.ail `macos_rules`): simulator devices and runtimes (`/Library/Developer/CoreSimulator`), Xcode device support, previews, docs cache, Aerial wallpapers and `/Library/Desktop Pictures`, macOS update leftovers, GarageBand and Logic libraries, Mail Downloads, VS Code caches. Kind `abs` rules apply under `/Library` even though that is protected.

Wanted from ail: a native folder picker for std.app (NSOpenPanel), and scan progress from `fs.scan`.

## Finding things (2026-11-08)

- **Sidebar** scrolls (wheel over it) and adds FIND (Large files over 100 MB, Old files not changed for a year) and FILE TYPES (Movies, Music, Pictures, Archives and disk images, Apps, Virtual machines, Documents, Code and build output, Other). Kind totals cover every scanned file (`kinds.totals`, hard links once); the lists show the biggest (`bridge.extras` keeps up to 60 per kind and 300 large and 300 old files below the size floor, with their folders).
- **Search** field next to Scan: names containing the text, anywhere in the scan; a matching folder hides the matches inside it.
- **Hover card** over a tile or row: name, size, safety, last change, kind, reason. It is anchored where the pointer entered, so moving inside a tile sends no new frame.
- **Right-click menu:** Reveal in Finder, Open, Copy Path, Show in Enclosing Folder (in a filtered view), Look Inside, Tick / Untick. Double-click a file reveals it.
- **Keys:** Up/Down select, Return looks inside or reveals, Space ticks, Escape cancels a sheet.
- The sheet dims the window with `Shade`. The frame is drawn once per event and clicks and moves are hit-tested against it.
