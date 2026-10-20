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


[MIT](LICENSE) for this project's code.
