# LanDashboard (WoW addon)

The in-game half of the 4L LAN progression dashboard: it records your character's levelling as you play so a small companion program can send it to the group's dashboard.

## What it is

A single-file addon (`LanDashboard/LanDashboard.lua`) that listens to a handful of game events and queues a line for each one into its SavedVariables file. It never talks to the network itself; addons can't. The [watcher](https://github.com/noftzjs/lan_dashboard_watcher) running on your PC reads that file and forwards new lines to the dashboard server.

This repository is published so players can read the code before installing it. The addon is developed inside the dashboard project and mirrored here on each release; the version in `LanDashboard.toc` is the one to compare against the zip you downloaded.

## What leaves your machine

Every record is one line in `WTF/Account/<account>/SavedVariables/LanDashboard.lua`, tagged with your character's full name. The watcher sends exactly these, nothing else:

| Record | When | Fields |
|---|---|---|
| `PROFILE` | login, zone change, guild change | faction, class, guild name |
| `ZONE` | entering a new zone | zone name |
| `XP` | any XP gain | level, current XP, XP to next level |
| `QUEST` | quest turned in | quest id, XP reward |
| `DEATH` | you die | level, zone |
| `STATUS` | login and level-up | gold, time played, item level, AFK time, professions, lifetime quest count |

Each line carries the in-game time it happened, so late syncs don't distort pace charts.

**Opt-outs.** Gold is private by default and stays off the dashboard until you turn sharing on. `/ldb private` lists what can be withheld; the settings panel (Interface Options, or `/ldb config`) has the same switches. Nothing about chat, friends, inventory contents, or other players is read.

## Commands

| Command | Does |
|---|---|
| `/ldb` | status: queued events, scoring, what will trigger the next sync prompt |
| `/ldb sync` | show the Sync button now |
| `/ldb config` | open the settings panel |
| `/ldb private` | show which fields are withheld; `/ldb private gold` toggles one |
| `/ldb verbose` | echo each queued event to chat, for debugging |
| `/ldb stats` | what this client exposes (used while developing) |
| `/ldb forget` | clear the local queue and start fresh (needed once when the server's database is reset) |

## How syncing works

SavedVariables are only written to disk when the UI reloads, so the addon scores "safe windows" (a flight path departing, going AFK, a loading screen) and shows a one-click Sync button when enough has happened to be worth flushing. By default it never reloads your UI on its own; the button is always your click. One opt-in setting, off by default, reloads once right after login.

## Install

The addon is on CurseForge as [LanDashboard](https://www.curseforge.com/wow/addons/landashboard), so the CurseForge app can install and update it. By hand, unzip so that you get `Interface/AddOns/LanDashboard/LanDashboard.lua` and `LanDashboard.toc`. The Interface number in the `.toc` matches the client build the LAN runs on; if the AddOns list shows it as out of date, tick **Load out of date AddOns**.
