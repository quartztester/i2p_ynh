I2P is administered entirely from its own console (YunoHost's SSO guards the door; the console itself needs no second login as long as you arrive through SSO). Useful from inside the console:

- **Status page** — "Network: OK" means peers can reach you; "Firewalled" means the peer port (\_\_port\_ext\_\_, TCP+UDP) is not forwarded to this server.
- **Config → Router manager** — bandwidth limits, and the *floodfill* toggle (this package enables floodfill by default; uncheck it to run as a plain relay). After toggling anything here the router must be restarted — the console offers a reboot button.
- **Logs & log settings** — the console log levels are per-logger; YunoHost also keeps journal output (`journalctl -u __APP__`).

Notes:

- Router identity (keys, netDB, config) lives in the app's data dir and is included in YunoHost app backups. Restoring a backup keeps the same router identity/reputation.
- The router's **own software updater is disabled on purpose**: updates come from the I2P apt repository via `yunohost app upgrade i2p`. Do not run the console's "update now" — it would overwrite dpkg-managed files.
- The console listens on loopback only; it is reachable exclusively through the SSO-gated nginx proxy.
