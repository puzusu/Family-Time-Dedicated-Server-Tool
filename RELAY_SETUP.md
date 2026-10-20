# Relay server (for the person who owns a VPS) - lets everybody host and join, behind ANY router or provider

Without a relay the program tries to open the router by itself (UPnP). Some connections cannot do that (your provider shares one address between customers, router without UPnP ...).
With a relay those hosts work too: the host's program connects OUT to your relay, friends connect to the relay, the relay passes the game traffic through. Nobody has to touch a router, firewall or VPN.

## 1. On the VPS (Windows or Linux, 1 CPU / 512 MB is plenty; traffic = the players' game traffic)
1. Copy `relay\FamilyTimeRelay` (Linux) or `relay\FamilyTimeRelay.exe` (Windows) to the VPS. Linux: `chmod +x FamilyTimeRelay`.
2. Run it once: `./FamilyTimeRelay`. It creates `relay.config.json` next to it with a **random Key** and starts. Stop it (Ctrl+C) if you want to change the ports:
   * `ControlPort` (default **7700**): where the hosts' programs connect.
   * `PortStart` - `PortEnd` (default **20000-20199**): one public port per host; friends connect to it. 200 hosts at most.
   * `MaxPlayersPerHost` 64, `MaxConnectionsPerIp` 12.
3. **Open these TCP ports** in the VPS provider's firewall (security group) and in the VPS's own firewall: `7700` and `20000-20199`.
   Linux example (ufw): `ufw allow 7700/tcp && ufw allow 20000:20199/tcp`.
4. Keep it running. Linux (systemd) - `/etc/systemd/system/ftrelay.service`:
   ```
   [Unit]
   Description=Family Time relay
   After=network.target
   [Service]
   WorkingDirectory=/opt/ftrelay
   ExecStart=/opt/ftrelay/FamilyTimeRelay
   Restart=always
   [Install]
   WantedBy=multi-user.target
   ```
   then `systemctl enable --now ftrelay`. Windows: run it in a console, or with a service wrapper / Task Scheduler "at startup".
5. The relay logs to the console and `relay.log`.

## 2. Tell the programs about it
Put a file **`relay.json`** next to `FamilyTimeMP.exe` (in the package you send to friends, before you zip it):
```
{ "Host": "your-vps-address-or-ip", "Port": 7700, "Key": "<the Key from relay.config.json>", "Always": false }
```
* `Always: false` - the program first tries to open the router; it uses the relay only when that is not possible. `Always: true` - always use the relay (simplest for support, adds the VPS hop to everybody's ping).
* Nothing else to configure. When a host presses START SERVER and the relay is needed, the program connects to it by itself, the invite shows the relay address and the host's own public port on the relay, and friends just paste the invite.
* The same host keeps the same public port forever (the program remembers a host id), so old invites stay valid.

## 3. Good to know
* The relay only forwards bytes to hosts that know the Key; it is not an open proxy. Anybody with the Key can register a host, so give the package only to people you trust (or change the Key and send a new `relay.json`).
* The game server still enforces its own password and abuse protection; the relay does not look inside the traffic. The traffic is not encrypted (as without the relay).
* The game server sees each friend as a different `127.x.y.z` address (derived from their real address), so its per-address limits and bans keep working per player.
* Test on one PC: `FamilyTimeRelay.exe`, then the program with a `relay.json` pointing at `127.0.0.1` (this is how the relay was tested).
