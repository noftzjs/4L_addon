# Backlog

## Publishing
- [ ] Push the first commit (repository created, remote set).
- [x] MIT licence added 2026-10-20.
- [x] CurseForge listing approved 2026-10-21: https://www.curseforge.com/wow/addons/landashboard, linked from the README and the dashboard's `/setup`.
- [x] Linked from the dashboard's `/setup` page (2026-10-20, in the uncommitted working tree).

## Keeping it in sync
- [ ] v3.10.1 (duplicate XP guard) is mirrored here but not yet released: push it and upload to CurseForge with the November build.
- [ ] Decide the mirror step: copy `LanDashboard/` from the dashboard repo and commit here on every addon version bump. The dashboard repo stays the source of truth because its Dockerfile and setup page build the zip from its own copy.
- [ ] Check the Interface number against the client build the LAN runs on, the week before 2026-11-04.
