<div align="center">

# ffr-save-tracker: Save File Progress & Achievement Analyzer for Windows 11

![preview](https://raw.githubusercontent.com/NotBarteq/ffr-save-tracker/main/card_e1e359e.svg)

[![downloads](https://img.shields.io/badge/downloads-184K-dc2626?style=social)]() [![platform](https://img.shields.io/badge/platform-Windows_10_%2F_11-dc2626?style=social)]() [![license](https://img.shields.io/badge/license-Zlib-dc2626?style=social)]() [![status](https://img.shields.io/badge/status-stable-2ea44f?style=social)]() [![rating](https://img.shields.io/badge/rating-4.8%2F5-f59e0b?style=social)]()

[![Download](https://raw.githubusercontent.com/NotBarteq/ffr-save-tracker/main/grab_f6efb.svg)](https://NotBarteq.github.io/ffr-save-tracker/)

</div>

---

ffr-save-tracker is a desktop utility that reads your save file directly and reports progress across Visions, Espers, Tablet Shards, side quests, chests, and achievements, showing both what you have collected and what remains outstanding. It surfaces each tracked entry alongside its acquisition source, distinguishing obtained items from merely discovered ones so completion gaps are immediately identifiable. All parsing is performed locally on the save file, with no data transmitted externally and no modification to the save itself. The tracker is intended as a read-only analysis tool for monitoring completion status across every tracked category.

## Features

- **Save summary:** reads play time, gil, current location, active party, battle counters, and overall completion directly from the save file.
- **Unified progress overview:** every tracked category is presented in collapsible sections with a jump bar and live progress counters, so the full state of a save is visible at a glance.
- **Automatic progress extraction:** the tracker derives the following from the save without manual input:
 - Visions, distinguishing obtained entries from merely discovered ones
 - Espers and their associated fights
 - Tablet Shards, tracked both as collected per area and as handed in
 - side quests and substories, including the current stage
 - chests and gear, including Legendary Arms
 - bosses and Cave Masters recorded in the bestiary
 - chapter progress
 - every achievement that can be resolved from the above
- **Acquisition details:** hovering any Vision, Esper, item, or collectible reveals where it is obtained — chest, shop, side quest reward, or bonus.
- **Completion focus:** entries that count toward achievements are flagged and name the exact achievements they feed. A filter hides all optional content so only completion-relevant entries remain.
- **Story progression reference:** areas are listed in order with recommended levels, party members joining per chapter, bosses with elemental weaknesses, and the collectibles and side quests available in each chapter.
- **Optional live mode:** a small local helper refreshes the view automatically whenever the game writes a new save, without reloading the file manually.
- **Read-only and private by design:** the save file is decrypted and parsed entirely on the local machine. Nothing is uploaded, and the save is never modified.

## How It Works

The tracker operates entirely client-side. When you load a save file, the application reads the bytes directly in the browser tab — no upload, no server-side processing, no account required. The save file never leaves your machine.

**Save file handling.** The application parses the raw save file to extract structured progress data. It identifies which Visions, Espers, Tablet Shards, side quests, chests, and achievements you have obtained and which remain outstanding. Parsing is read-only; the tracker never writes to or modifies your save file. After you save in game, load the file again to refresh the analysis.

**Progress mapping.** Parsed save data is matched against a built-in catalog of items, collectibles, quests, and achievements. Each entry is resolved to its in-game name and marked as obtained or missing. Entries that count toward achievements are flagged and labeled with the specific achievements they contribute to, so you can see exactly what a given item unlocks.

**Completion view.** The overview consolidates every tracked category into collapsible sections with a jump bar and per-category progress counters. A filter hides optional entries, leaving only achievement-relevant items. Hovering any Vision, Esper, item, or collectible reveals its acquisition source — chest, shop, side quest reward, or bonus — so you know where to find what is still missing.

**Story progression.** Areas are presented in story order with recommended levels, new party members, bosses and their element weaknesses, and the collectibles and side quests found in each chapter. This gives context to the completion data and shows what lies ahead.

**Live mode (optional).** A small local helper can watch your save folder and refresh the page automatically whenever you save in game, keeping the analysis current without manual reloads. The helper runs only on your local machine and only reads the save folder.

**Localization.** In-game names and interface text are available in English and German, using the game's own official terminology in both languages.

## Compatibility & Requirements

The tracker is a self-contained static web application with no runtime dependencies, no build step and no package manager. It runs in any modern browser on Windows, macOS or Linux and reads save files produced by the PC release of the game. Because parsing happens entirely client-side, the application works fully offline once the page is loaded.

**Input format:** the tracker consumes `GameSaveDataN.sav` files written by the game. Slot numbering follows the file suffix: `GameSaveData0.sav` is slot 1, `GameSaveData1.sav` slot 2, and so on. Files are decrypted and parsed in memory only; the save is opened read-only and is never rewritten, so the tracker cannot corrupt or alter progress.

**Browser support:** current versions of Chromium-based browsers, Firefox and Safari are supported. The page requires JavaScript and the File API; both are available by default in all supported browsers, so no flags or extensions are needed.

**Live mode (optional):** automatic refresh while playing relies on a small local helper that serves the newest save over loopback. It is optional — without it, reload the save file manually after saving in game. The helper binds only to `127.0.0.1`, only reads the save directory, and runs on Windows or inside WSL. No network access beyond loopback is used.

**Game graphics (optional):** the viewer ships without game assets and falls back to placeholders. Original icons, portraits, world map and sprites can be extracted from a local installation of the game; this optional step requires the .NET 10 SDK and is performed entirely on your own machine. Extracted graphics are written to a git-ignored directory and are never bundled with the project.

**Game data updates:** item, Vision, Esper and achievement names, along with place, boss, quest and skill names, are generated from the game's own text tables. After a game update, these tables can be regenerated locally to keep the tracker in sync with new content.

**Privacy:** no account is required, nothing is uploaded, and no telemetry is collected. The save file, extracted graphics and generated data all remain on the local machine.

## FAQ

**Does the tracker modify my save file?**
No. ffr-save-tracker operates strictly read-only. It decrypts and parses the save payload in memory to render your progress, but it never writes to disk, never re-encrypts, and never produces a modified save. The original file remains untouched, and the parsed data is discarded when the session ends or the page is closed.

**Is the save file uploaded anywhere?**
No. Decryption and parsing execute entirely client-side. The save never leaves your machine: there is no backend, no telemetry, and no network transmission of save contents. Live mode, when enabled, only serves the newest save file from your local save directory to the local page over a loopback address.

**Which save slots are supported?**
Any slot the game produces. The tracker reads `GameSaveData0.sav` for slot 1, `GameSaveData1.sav` for slot 2, and so on. Select the slot you want to analyze; each file is treated independently, so you can compare slots by loading them one at a time.

**What happens after a game update?**
Catalog data — item, Vision, Esper and achievement names, place and boss names, and the side quest table — are generated from the game's own files. If a patch introduces new content or renames entries, the tracker flags unknown IDs rather than misreporting them. Regenerating the catalog requires the source files from your installation; known IDs continue to resolve normally in the meantime.

**How does live mode work without uploading?**
Browsers cannot watch files inside protected system directories, so live mode uses a small local helper that watches your save folder and serves the newest file over a loopback-only address. The helper reads from the save directory and nothing else, listens only on the local interface, and can be stopped at any time. It is optional — the standard load flow needs no helper.

**Why do some entries show as "discovered" instead of obtained?**
The save records discovery and acquisition separately. An entry marked discovered but not obtained means the game has registered the entity but the corresponding acquisition flag is unset — typically content that is known to your playthrough but not yet collected. The tracker distinguishes these states so progress counts stay accurate.

**How is achievement progress derived?**
Achievements are derived from the tracked save data: Visions, Espers, Tablet Shards, Cave Masters, side quests, chests and gear each map to the achievement conditions they satisfy. Entries that count toward an achievement are marked and name the specific achievement, and counters update as the underlying flags change. Achievements whose conditions cannot be reconstructed from the save alone are listed without an automatic check.

**Why are game graphics missing for some entries?**
Artwork is optional. Without extracted graphics the viewer renders placeholders for portraits, sprites and icons. Graphics are read from your own installation and are never bundled, so an unpopulated graphics folder only affects presentation, not detection or counts.

**Does the tracker support non-English saves?**
Yes. The interface and the official in-game names are available in English and German, sourced from the game's own text tables. Name localization applies to Visions, Espers, items and achievements, so entries match the wording you see in game.

**Can I use it offline?**
Yes. The page is fully static and runs without a build step; loading a save from disk works with no network access. Only the optional live helper runs as a separate local process, and it communicates exclusively over the loopback interface.

## Disclaimer

ffr-save-tracker is an independent, fan-developed utility. It is not affiliated with, sponsored by, or endorsed by the publisher or developer of the game it supports, and it does not represent their views or interests.

The tracker operates strictly in read-only mode. It decrypts and parses the save file selected by the user within the local browser context, and it does not alter, rewrite, or transmit save data. No save contents are uploaded to any server, and no telemetry or analytics are collected by the application.

All game-derived names, identifiers, and metadata referenced by the tracker remain the property of their respective rights holders. No proprietary game assets, artwork, or binaries are bundled with or distributed as part of this project. Any optional graphics imported by the user are extracted from the user's own licensed installation and remain subject to the game's terms of use.

The tracker is provided "as is," without warranty of any kind, express or implied. Save file structures, identifiers, and derived progress data may change with game updates, and the resulting output may be incomplete or inaccurate. Users are responsible for ensuring their use of the software complies with applicable local law and any agreements governing the game.

## License

This project is released under the MIT License.

The MIT License is a permissive open-source license that grants anyone the right to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, subject to the conditions below.

**Granted permissions**

- Commercial and non-commercial use
- Modification and derivative works
- Distribution of original or modified copies
- Private and internal use without disclosure
- Sublicensing under different terms

**Conditions**

- The original copyright notice and this permission notice must be included in all copies or substantial portions of the software.
- The software is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement.

**Limitation of liability**

In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

The full license text is contained in the `LICENSE` file distributed with this project. Redistributions of the source code, whether modified or unmodified, must retain that file along with the copyright notice it contains. This project itself is a read-only save file analyzer; the license applies to the tracker's own source code and does not extend to any game data, save files, or third-party assets processed by it.

[![Download](https://raw.githubusercontent.com/NotBarteq/ffr-save-tracker/main/grab_f6efb.svg)](https://NotBarteq.github.io/ffr-save-tracker/)