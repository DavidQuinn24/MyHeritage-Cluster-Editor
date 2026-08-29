# AutoClusters Editor

Add persistent notes, cluster names, research status, and surname tags to a MyHeritage AutoClusters DNA-match export — without ever modifying MyHeritage's original files.

## What this is

MyHeritage's AutoClusters export (CSV + interactive HTML) is a read-only snapshot of your DNA match clusters. There's no way to name a cluster, leave a research note, or tag a match's status, and re-running the analysis produces a fresh set of files each time. AutoClusters Editor is a single HTML file that reads that export and layers an editable research workspace on top of it, saving your notes to a companion JSON file it creates alongside the export. It never edits or overwrites MyHeritage's own files.

## Requirements

- A modern browser. Chrome or Edge is recommended — see "Autosave vs. manual save" below.
- An internet connection while the tool is open. It loads its charting and table libraries live from MyHeritage's own CDN rather than bundling them, so it won't render correctly on a fully offline or locked-down network.

## Installation

There isn't one. Download `AutoClusters Editor.html` and save it into the same folder as your MyHeritage AutoClusters export (the folder containing the export's CSV, HTML, and ReadMe PDF). Double-click it to open it in your browser.

## Usage

1. Open `AutoClusters Editor.html`.
2. Click "Open export folder" and select the folder containing your MyHeritage export (Chrome/Edge). If that doesn't work, or you're on a browser without folder-picker support, use the manual file pickers instead.
3. The tool reads your export's matches and clusters and creates `clusters-metadata.json` in that folder the first time you open it there.
4. Edit any cluster's name, surname/line, or notes, and any match's notes, research status, or surname. Changes save automatically back into `clusters-metadata.json`.
5. Reopen the tool and point it at the same folder any time to pick up where you left off. If MyHeritage regenerates the export later, per-match notes carry over automatically (matched by MyHeritage's own stable match ID); cluster names and notes stay tied to the old cluster numbers, since cluster numbering can shift between exports, so give those a quick manual check after a refresh.

## Autosave vs. manual save

Chrome and Edge support direct-to-disk autosave via the browser's File System Access API: once you grant folder access, every edit is written straight to `clusters-metadata.json` with no further action needed. A status indicator confirms it's saving.

Other browsers (Firefox, Safari) don't support that API, so the tool falls back to manual pickers for loading and an "Export metadata" button for saving. On those browsers you'll need to re-export and keep the downloaded file after making changes, since nothing saves automatically.

## What gets added to your export folder

- `AutoClusters Editor.html` — this tool (you place it there)
- `clusters-metadata.json` — created automatically on first open; holds your custom cluster names, notes, research statuses, and surname tags
- `clusters-metadata.backup.json` — a safety copy the tool writes automatically before it touches an existing metadata file, in case something goes wrong

## What this tool never does

- Never modifies MyHeritage's original CSV, HTML, or PDF export files
- Never overwrites `clusters-metadata.json` without first backing it up
- Never sends your data anywhere — everything stays local to your machine, and it only reads the files you point it at
