# Administering I2P

The router is managed entirely from its own web console. YunoHost's SSO guards the
door — arriving through the portal, the console needs no second login.

## First steps after install

1. Open the console and check the **status page**.
   - **Network: OK** — peers can reach you. You're done.
   - **Firewalled** — the peer port is not reachable from outside; see Ports below.
2. Optionally review *Config → Router manager* for bandwidth limits and relay role.

## Ports

| Purpose | Port | Notes |
|---|---|---|
| Peer transport | `__port_ext__` (TCP **and** UDP) | Must be port-forwarded on your router, or the console reports *Firewalled* and the relay contributes far less. |
| Console | loopback only | Never directly exposed; reachable exclusively through the SSO-gated nginx proxy. |

## Routine settings (inside the console)

- **Bandwidth limits & relay role** — *Config → Router manager*. This package enables
  *floodfill* (a name/database-sharing volunteer role) by default; uncheck it to run
  as a plain relay. Any change here requires a router restart — the console offers a
  reboot button.
- **Log verbosity** — *Logs & log settings* is per-logger. The systemd journal keeps
  the process-side output: `journalctl -u __APP__`.

## Updates

The router's **own software updater is deliberately disabled**: updates arrive from
the I2P apt repository via `yunohost app upgrade i2p`. Do not use the console's
"update now" — it would overwrite dpkg-managed files and break the package.

## Data & identity

Router identity (keys, netDB, configuration) lives in the app data dir and is
included in YunoHost app backups. Restoring a backup therefore preserves the same
router identity and its accumulated reputation.

## Troubleshooting

| Symptom | Cause & fix |
|---|---|
| Console shows **Firewalled** | Peer port `__port_ext__` (TCP+UDP) is missing a router port-forward, or the domain's DNS record is Cloudflare-proxied (must be DNS-only for raw ports). |
| I2PSnark (torrent UI) reports *"Configured i2psnark directory ... does not exist"* | Its per-app config holds a stale absolute path. The correct value is relative: `i2psnark.dir=i2psnark` in `i2psnark.config.d/i2psnark.config` inside the data dir. Restart the router after editing. |
| Router slow after boot | Normal on first boot: it performs a large netDB re-check; watch `journalctl -u __APP__`. |
| Router not running | `systemctl status __APP__`; the unit restarts itself on failure (exit 143 on stop is a clean JVM shutdown, not an error). |
