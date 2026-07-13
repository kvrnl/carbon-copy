# CarbonCopy

**Real-time folder backup for Windows.** CarbonCopy quietly mirrors the folders you care about to up to two destinations — an external drive, a network drive, another folder — and keeps them in sync the moment files change. It runs in the system tray and stays out of your way.

> Made by [KVRNL](https://kvrnl.com)

---

## What it does

- **Live mirroring** — the instant you save, rename, or delete a file in a watched folder, the change is copied to your backups (usually within about a second).
- **Two destinations** — keep a copy on, say, an external SSD *and* a network drive, so you always have a spare.
- **Safety-net sweep** — a periodic background scan catches anything missed, including changes made while the app (or a drive) was offline.
- **Recoverable deletes** — deleting a file moves its backup copy to a dated Recycle Bin inside the destination, kept for a retention period you choose.
- **Turbo mode** — temporarily speeds up large transfers, then switches itself back off.
- **Automatic updates** — checks for new versions hourly and installs them silently in the background.
- **Tray app** — lives by the clock, starts with Windows (optional), and never nags you.

CarbonCopy is a **one-way mirror**: your source folders are the source of truth and are only ever **read** — never modified or deleted. All writing and deleting happens inside the destination folders.

---

## Download & install

1. Grab the latest **`CarbonCopy-x.y.z-Setup.exe`** from the [**Releases**](../../releases/latest) page.
2. Run it. Windows may show a blue *"Windows protected your PC"* screen because the app isn't code-signed — click **More info → Run anyway**.
3. Follow the installer. It installs per-user (no admin needed) and can create a desktop shortcut and start with Windows.

That's it — CarbonCopy opens and drops into your system tray.

---

## Quick start

1. On the **Dashboard**, click **+ Add Folder** and choose a folder you want protected. Add as many as you like.
2. Under **Destination 1**, click **Change Path** and pick where backups should go. Add a second destination too if you want two copies.
3. Flip each destination's toggle **ON**. Done — CarbonCopy keeps everything in sync automatically.

Your files are mirrored into a subfolder named after each source folder (e.g. source `C:\Work` lands at `D:\Backup\Work\…`), so multiple sources never collide.

---

## How it works

**Real time + a safety net.** A file watcher copies changes the instant they happen. On top of that, a periodic *sweep* re-checks every file (size + modified-time) and fixes anything that drifted — for example, edits made while CarbonCopy was closed or a destination was unplugged.

**Source folders.** Only ever read. Use **Pause** to stop watching a folder temporarily, or **Remove** to stop backing it up (files already copied to your destinations are kept).

**Destinations.** Up to two. The colored dot shows status — blue = connected and syncing, orange = paused/waiting, red = offline, gray = disabled. If a drive drops out, the destination pauses and a **Reconnect** button appears; click it once the drive is back and CarbonCopy catches up.

**Deleting files & the Recycle Bin.** When a file is removed from a source, its backup copy isn't erased — it's moved into a `Recycle Bin` folder inside the destination, organized by date, and kept for the **retention period** (set in Settings) before being cleared. Accidental deletes are recoverable.

**Turbo mode.** Temporarily copies more files at once with bigger buffers to push large transfers faster. It turns itself back off automatically after the time limit.

---

## Settings

- **Sweep interval** — how often the background safety scan runs.
- **Recycle Bin retention** — how long deleted files are kept before being cleared.
- **Exclude patterns** — folder/file names to skip (e.g. `node_modules`, `.git`, `Thumbs.db`).
- **Debounce & concurrent copies** — fine-tune responsiveness and speed.
- **Turbo** — parallel transfers, buffer size, and time limit.
- **Start with Windows**, notifications, and **Export / Import** to move your setup to another PC.

---

## Automatic updates

CarbonCopy checks this repository's Releases about every hour. When a newer version is published, it downloads the installer and updates itself silently in the background — closing, upgrading, and relaunching to the tray with no interruption. You can also trigger a check anytime via **Check for Updates** on the Settings tab.

---

## Running in the background

Closing the window doesn't quit CarbonCopy — it tucks into the system tray and keeps backing up. **Right-click the tray icon** for *Open Dashboard*, *Pause All*, or *Exit*.

If a file ever can't be backed up, the reason is recorded in a log at:

```
%AppData%\CarbonCopy\errors.log
```

Your settings live at `%AppData%\CarbonCopy\config.json`.

---

## Notes

- **Windows / .NET.** Self-contained build — no separate .NET install required.
- **One-way mirror.** Destinations are made to match the source. A file that exists in a destination's mirror folder but no longer in the source is moved to the Recycle Bin; a destination file that differs from the source is replaced by the source version.
- **Not code-signed (yet).** SmartScreen will warn on first run — *More info → Run anyway*.

---

© KVRNL
