# Family Time Multiplayer - quick start

Open **`FamilyTimeMP.exe`** (the program in this folder). It does everything: no console, no config files, no router knowledge needed.
Needs: **Family Time Ep. 3, build b108, Windows 10/11, a DirectX 12 graphics card**. Everybody (host and friends) must use the same download of this program.

## I want to play on a friend's server
1. **Step 1** - press **Find it for me** (or **Browse...**) and pick your Family Time folder (the one with `FamilyTime.exe`). It must say "Family Time found".
2. **Play tab, step 2** - press **Install the mod**. (Once. **Remove the mod** puts the original game back.)
3. **Step 3** - press **Paste invite from my friend** (your friend sends you the invite text), type **your name**, press **PLAY**. The game starts and connects by itself.

## I want to host a server for my friends
1. **Step 1** - choose your Family Time folder (same as above).
2. **Host tab, A** - press **Prepare the server** once (about a minute; it makes the server its own copy of the game, yours stays untouched).
3. **B** - choose a **server name** and **password**, press **Save settings**.
4. **D** - press **START SERVER**. The first time, Windows asks for permission once (choose Yes): the program opens the Windows Firewall and asks your router to open the connection by itself. The log (black box) tells you if friends anywhere can join.
5. **C** - press **Copy invite for friends** and send the text to them. They only paste it into their program.
6. You can play too: **Play on my own server**. **Stop server** saves the world. The other buttons: save the world now, skip the night, rain on/off, flash flood, backup, kick a player.

## If a friend cannot connect
* Same house: choose "Home network" in C and send a new invite.
* Other house: START SERVER sets the connection up by itself. If a `relay.json` came with the program, a connection that cannot be opened directly is automatically routed through the relay server (nothing to do).  If the log says the router did not allow it, switch **UPnP** on in your router's settings (most routers have it) and press START SERVER again. If it says your internet provider shares one address between customers, direct hosting is not possible on that connection: let a friend with a normal connection host.
* "protocol mismatch" / "mod version mismatch": everybody must use the same download and press **Install the mod** again. "game build mismatch": everybody needs Family Time **b108**.
* The first join takes a moment (the world is downloaded once). The game sometimes freezes at launch (also without the mod): close it and start again.
* Logs: this program's folder (`logs`), `server_game\FamilyTimeMP\ftmp-server.log`; players: `<game folder>\FamilyTimeMP\ftmp-local.log`.

## In the game
**F10** connect / disconnect, **T** chat. The night starts when everybody is in bed (the host can skip it). Disconnecting saves your colony on the server.

---

## Updating to a newer version

Replace `FamilyTimeMP.exe` with the new one and open it. Nothing else is needed:

* **Your world and everybody's colonies stay.** They are saved on the host's PC, not in the program, and an update never touches them.
* **Players:** press **Install the mod** once (it updates the mod in your game folder). Everybody must use the same version, otherwise the join says "mod version mismatch".
* **The host:** just press **START SERVER**. If the program is newer than the server's mod, the server updates itself first (the saved world is kept).
* If the old version came as a folder with `server_game` next to the program, put the new `FamilyTimeMP.exe` into that same folder: it keeps using that server and its world.
