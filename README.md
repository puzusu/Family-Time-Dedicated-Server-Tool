# Family Time Multiplayer

Private co-op for **Family Time Ep. 3 (build b108, Windows DX12)**: everyone runs their own colony (their own Wolf Mama and pups),
a server holds the shared world, and the night starts when everybody has put their pups to bed.

*Developed by Puzusu for the Family Time community, with much love.*

*Thanks to our testers: GROM and SuperStore.*

> You need your own copy of the game. Nothing of the game is in this repository; the mod patches **your** files.
> Mod 0.3.3 works with game build **b108** only.

## Play (no technical knowledge needed)

1. Download **`FamilyTimeMP.exe`** from the [Releases](../../releases) page. It is a single file; just run it.
   (Windows may warn about an unknown publisher: *More info → Run anyway*. The exe is not code-signed.)
2. **Play tab:** choose your Family Time folder (or *Find it for me*), press **Install the mod** once.
3. To join a friend: press **Paste invite from my friend**, then **PLAY**.
4. To host: **Host tab** → *Prepare the server* → *START SERVER* → *Copy invite for friends*. The program opens the
   Windows Firewall rule and asks the router to open the port by itself (UPnP / NAT-PMP).

Step-by-step with pictures of every button: [docs/QUICK_START.md](docs/QUICK_START.md).

## What it does

- Shared world and per-player colonies, held by the server by player name (reconnect = same colony).
- Shared ground items and held items, shared water simulation, rain and floods, sleep/night voting.
- Colony looks (32 plain colours), player avatar model, wolf-mom carry animations.
- Dedicated server: the same game exe running headless, plus a supervisor (console launcher or the GUI).
- Optional **relay** for hosts whose connection can't be opened directly (CGNAT etc.): [docs/RELAY_SETUP.md](docs/RELAY_SETUP.md).

## Repository layout

| Folder | What |
|---|---|
| `src/FamilyTimeMP` | the mod (patched into the game's `Assembly-CSharp.dll` by a Mono.Cecil weaver) |
| `src/Shared` | protocol shared by mod, server and tools |
| `src/ServerLauncher` | dedicated-server supervisor (console) |
| `src/Manager` | `FamilyTimeMP.exe`, the click-and-play window (WinForms, built from the UI mockups in `src/Manager/Assets`) |
| `src/Relay`, `src/RelayCore` | the relay server and the host-side agent |
| `tools/Patcher` | the weaver / verifier |
| `tools/*.ps1` | build, packaging and test scripts (bot-driven end-to-end tests) |
| `docs/` | quick start, relay setup, design and protocol notes |

## Build from source

Requirements: Windows 10/11, .NET 8 SDK, a DX12 GPU (to run the tests), and **your own copy of Family Time b108**.

1. Copy your game folder to `game\` in the repo root (the folder that contains `FamilyTime.exe`). It is git-ignored.
2. `powershell -File tools\build_modded.ps1` builds the mod and a patched copy in `game_modded\`.
3. `powershell -File tools\package_dist.ps1` builds everything and writes the single-file `dist\FamilyTimeMP.exe`
   (the other files go to `dist_extra\`).
4. The player-avatar files (`samples\peasant_avatar.glb/.cfg`) are not in the repo (they contain third-party animation data).
   Without them the package script fails at the copy step: put your own `.glb` there (see [docs/CUSTOM_AVATARS.md](docs/CUSTOM_AVATARS.md)),
   or remove those two lines from `tools\package_dist.ps1`.
5. Optional: create `dist_src\relay.json` (`{"Host":"...","Port":7700,"Key":"..."}`) before packaging to embed a relay for your community.

Tests (examples): `tools\run_mp_test.ps1`, `tools\test_relay.ps1`, `tools\test_manager_ui.ps1`. They start the real game headless and need the `game_modded\` copy.

## Third-party

- [Mono.Cecil](https://github.com/jbevain/cecil) (MIT) is used by the patcher.
- Unity and Family Time belong to their respective owners; no game assets are distributed here.

## Licence

[MIT](LICENSE) for this project's code.
