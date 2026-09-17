# 💙 File Tags Native

**Current portable build: 1.0.9** — Windows x64, self-contained and unsigned.

File Tags Native is a local Windows desktop application for browsing Desktop and Downloads and assigning private descriptors and tags to files and folders without modifying their ordinary contents.

## Data safety and privacy

- No account is required.
- Filenames, paths, descriptors, and tags are not uploaded.
- No telemetry is collected.
- Network access is only intended for update checks, if enabled in a future version.
- File Tags does not rename, move, or delete ordinary files or folders.
- Administrator privileges are not required during normal use.

Metadata is stored in NTFS alternate data streams (ADS), with SQLite serving as a rebuildable search index. Files and folders can both be tagged. Streams may be lost when items are copied to FAT32/exFAT drives, some cloud services, archives, or systems that do not preserve them. Folder ADS is especially dependent on the copy tool preserving directory streams. Use **Data & Safety → Export JSON backup** before moving important items.

The Data & Safety screen can export and restore readable JSON backups, detect ADS support, rebuild the SQLite index from Desktop and Downloads, and report missing or unhealthy metadata. Metadata removal for an individual file or folder is available from its right-click menu. Export a backup before moving important tagged items.

## Screenshots

### Main file browser

![File Tags main file browser](docs/images/file-tags-main.png)

### Quick metadata editor

<img src="docs/images/file-tags-quick-editor.png" alt="File Tags quick metadata editor" width="520">

## Launch

For the portable release, download `FileTags-v1.0.9-win-x64-portable.zip` from [GitHub Releases](https://github.com/NanditaVenkur/file-context/releases), verify its accompanying SHA-256 checksum, extract the ZIP, and run `FileTags.exe`. The .NET SDK/runtime is not needed. Keep the extracted folder in place while Explorer integration is enabled; if you move it, disable and re-enable the command from the new location. The local development copy can also be launched with the **File Tags** Desktop shortcut.

## Current features

- Native dark WPF interface with Details and Grid views.
- Scroll vertically over the file list with a mouse wheel or two-finger touchpad gesture, and horizontally in Details view with a left/right two-finger gesture; scrollbars remain available.
- Desktop, Downloads, subfolder, Back, and Recent navigation.
- **All tags** shows indexed tagged files and folders across Desktop and Downloads, including subfolders. Enter a tag to filter to exact matches; the absolute path is shown for each result.
- Recent activity is retained for 18 days and capped at the newest 50 entries.
- Descriptors and tags stored in each file or folder's NTFS alternate data stream named `FileTags`.
- SQLite retained as a rebuildable search/index cache rather than the metadata source of truth.
- Collapsible metadata editor and tag badges.
- Created, Modified, Size, Type, Status, and metadata columns.
- Search across name, descriptor, tags, file type, availability, and absolute path.
- Dynamic search placeholder showing the current folder, Recent, or All tags scope.
- Folder search remains scoped to the open folder. The All tags view uses the local SQLite index; if older ADS metadata is missing there, use **Data & Safety → Rebuild index** to discover it.
- Sorting by name, modified date, created date, size, or descriptor.
- Grouping by created day, file type, availability, or modified-time period. The default is newest creation date, grouped by day.
- Resizable Details columns using the dividers between column headings.
- Clickable Details rows and a row/card context menu for copying the quoted absolute path, name, descriptor, or tags.
- Cohesive dark rounded context menus and reliable standard Windows scrollbars rendered through WPF's dark theme.
- Stable Windows file identity and scoped Desktop/Downloads monitoring for same-drive renames and moves.
- Missing-file preservation in Recent.
- `Ctrl +`, `Ctrl -`, and `Ctrl 0` text scaling.
- Layered dark gradients, rounded focus-aware inputs, subtle transparency, and restrained entrance/panel animations.
- Double-click files to open them with their normal Windows application.
- An optional current-user Explorer command, **Edit File Tags**, opens a compact native ADS editor from Windows 11 **Show more options** for a selected file or folder.
- The compact editor has scrollable content with a fixed action bar and can save descriptor/tags or hand the selected item off to the full app with **View in File Tags**. Press Enter to save; Shift+Enter inserts a newline in the descriptor. A successful save closes the compact editor or collapses the editor in the main app.

## Metadata and safety

The source metadata is UTF-8 JSON in `<item>:FileTags`. Ordinary file contents remain unchanged, but the NTFS file or folder gains or updates this named stream. The index is stored at `%LOCALAPPDATA%\FileTagsNative\metadata-test.db` and can be rebuilt from intact ADS under Desktop and Downloads, including subfolders. Recent activity is stored only in SQLite and is not recovered by an index rebuild. Existing SQLite-only descriptions and tags migrate lazily into ADS when their items are encountered. The app does not write to the original browser-based File Tags database and exposes no filesystem rename, move, copy, or delete commands; its Copy commands only place text on the Windows clipboard.

## Explorer command

The local development copy has `FileTagsLauncher.exe`, a no-console launcher that reads `current-app.txt` and forwards arguments to the current versioned build. The portable ZIP contains a self-contained `FileTags.exe` instead. The optional Explorer integration registers **Edit File Tags** for the current user for selected files and folders. It can be disabled in Data & Safety. The static verb normally appears under **Show more options** on Windows 11; no code is loaded inside Explorer and no administrator access is required.

## Current limitations

- Cross-drive and USB moves are not reconnected automatically.
- ADS may be lost when copying to non-NTFS filesystems or through tools that ignore named streams.
- Programs that replace a file during Save may replace its ADS as well.
- Missing entries do not yet have a Locate File workflow.
- Icons are currently simple placeholders except for the application icon.
- Open With and an installer are deferred; the current release is portable.
- The portable release is not digitally signed, so Windows may show an Unknown publisher or SmartScreen warning. Verify the release checksum before running it.
- Primary-menu Windows 11 integration is deferred; the safe static verb appears under **Show more options**.

See `PROJECT_STATUS.md` for detailed progress and safety boundaries. See `FEATURE_IDEAS.md` for the prioritized product roadmap and future feature concepts.
