# Husk GUI

One `std.app` canvas (`husk.ail`, `view/view.ail`), Safari-style dark like Garlic.

- **Sidebar:** volume usage bar (green slice = what the current selection would free), Overview, Safe to delete, categories with sizes.
- **Toolbar:** clickable breadcrumb; scan progress bar while `pct < 1` (fed by `external` events `scan` with `pct|files|path`), else Rescan.
- **Treemap** (`treemap/`, squarified, tested): tiles colored green / amber / red by safety; click selects, click a selected folder drills in.
- **List:** sortable Name / Size / Safety, size bars, safety badge, reason, tick boxes; scrolls.
- **Detail band:** reason, size, last used, full path of the selected item.
- **Footer + sheet:** "Select all safe", "Review & Move to Trash…" opens a sheet listing exactly what goes; Undo after.
- **Keys:** Backspace goes up, Escape closes the sheet.

`model/` is a MOCK tree. The core lane's model replaces it; the GUI needs `Entry{name,size,is_dir,safety,reason,cat,parent,kids,age}`.

## Needed in ail (not worked around)

1. `fs.trash` (the sheet's Move to Trash only hides entries now), `fs.scan` progress events, `fs.volume`.
2. std.app: a canvas `move` (hover) event for treemap tooltips; double-click; right-click context menu; alpha in `Fill` for a dimmed sheet backdrop; host-side text measuring is there (std.app.13) and should replace `look.width`.

Not built or run yet: builds happen on Kaleb's machines.
