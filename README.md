<img width="1557" height="966" alt="Image" src="https://github.com/user-attachments/assets/ddc4dfe2-be23-459c-8ce3-db879028626b" />

# AutoClusters Editor

Add persistent notes, cluster names, research status, and surname tags to a MyHeritage AutoClusters DNA-match export — without ever modifying MyHeritage's original files.

## What this is

MyHeritage's AutoClusters export (CSV + interactive HTML) is a read-only snapshot of your DNA match clusters. There's no way to name a cluster, leave a research note, or tag a match's status, and re-running the analysis produces a fresh set of files each time. AutoClusters Editor is a single HTML file that reads that export and layers an editable research workspace on top of it, saving your notes to a companion JSON file it creates alongside the export. It never edits or overwrites MyHeritage's own files.

## Requirements

- A modern browser. Chrome or Edge is recommended — see "Autosave vs. manual save" below.
- An internet connection while the tool is open. It loads its charting and table libraries live from MyHeritage's own CDN rather than bundling them, so it won't render correctly on a fully offline or locked-down network.

## Installation

There isn't one. Download `Autocluster-Editor.html` and save it into the same folder as your MyHeritage AutoClusters export (the folder containing the export's CSV, HTML, and ReadMe PDF). Double-click it to open it in your browser.

## Usage

1. Open `Autocluster-Editor.html`.
2. Click "Open export folder" and select the folder containing your MyHeritage export (Chrome/Edge). If that doesn't work, or you're on a browser without folder-picker support, use the manual file pickers instead.
3. The tool reads your export's matches and clusters and creates `clusters-metadata.json` in that folder the first time you open it there.
4. Edit any cluster's name, side, status, surname/line, or notes, and any match's notes, research status, or surname. Changes save automatically back into `clusters-metadata.json`.
5. Reopen the tool and point it at the same folder any time to pick up where you left off. If MyHeritage regenerates the export later, per-match notes carry over automatically (matched by MyHeritage's own stable match ID); cluster names and notes stay tied to the old cluster numbers, since cluster numbering can shift between exports, so give those a quick manual check after a refresh.

## Paternal / Maternal / Both

Each cluster has a Side field (blank / Paternal / Maternal / Both) — a common source of confusion when working AutoClusters is not knowing which side of the family a cluster belongs to, so this tags it once and shows it everywhere that cluster is already named: the matrix legend, the table's Cluster column, and the two panels below. Individual matches can optionally override their cluster's side for the rare exception (a match that doesn't fit its cluster); leave it blank to just inherit the cluster's side.

## Cluster Bridge Hints and Next Steps

Two collapsed panels sit below "Your clusters":

**Cluster Bridge Hints** lists matches that share DNA with a different cluster than their own ("bridges") — MyHeritage's matrix already shows these as faint gray cells, this just ranks and surfaces the ones worth a look. A bridge gets a subtle green outline in the matrix if one of the two matches involved is marked Identified, or amber if one of their whole clusters is marked Identified (a specific identified person always outranks a general cluster match). Hovering any bridge cell in the matrix also shows which two clusters it connects.

**Next Steps** turns the same information into plain-language suggestions: focus on identifying someone in a large cluster with no leads yet, investigate a cluster pair with many bridge matches (solving one might solve both), or consider tagging a cluster's Side after a strong bridge to an already-tagged cluster.

Both panels are collapsed by default and stay out of the way until you open them. Dismiss any hint or suggestion with its × once you've looked at it — dismissals are saved, so they won't keep reappearing — and use each panel's "Show dismissed … again" button if you want them back.

## Autosave vs. manual save

Chrome and Edge support direct-to-disk autosave via the browser's File System Access API: once you grant folder access, every edit is written straight to `clusters-metadata.json` with no further action needed. A status indicator confirms it's saving.

Other browsers (Firefox, Safari) don't support that API, so the tool falls back to manual pickers for loading and an "Export metadata" button for saving. On those browsers you'll need to re-export and keep the downloaded file after making changes, since nothing saves automatically.

## What gets added to your export folder

- `Autocluster-Editor.html` — this tool (you place it there)
- `clusters-metadata.json` — created automatically on first open; holds your custom cluster names, notes, research statuses, and surname tags
- `clusters-metadata.backup.json` — a safety copy the tool writes automatically before it touches an existing metadata file, in case something goes wrong

## What this tool never does

- Never modifies MyHeritage's original CSV, HTML, or PDF export files
- Never overwrites `clusters-metadata.json` without first backing it up
- Never sends your data anywhere — everything stays local to your machine, and it only reads the files you point it at
