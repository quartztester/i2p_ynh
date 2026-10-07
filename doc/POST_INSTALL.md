# After installation

I2P is installed and running. This page summarizes what to check first.

## Access the console

**https://`__DOMAIN__`/** — gated behind YunoHost's SSO, so only users of your
portal can reach it. No second login is required when arriving through the portal.

## Required next step: open the peer port

For the router to act as a useful relay, forward port **`__PORT_EXT__` (TCP *and*
UDP)** on your internet box/router to this server.

Verify in the console's **status page**:

| Status shown | Meaning |
|---|---|
| **Network: OK** | Peers can reach you — nothing more to do. |
| **Firewalled** | The port forward is missing or wrong; the relay contributes much less until fixed. |

If your DNS for this host goes through a proxy/CDN (e.g. Cloudflare orange-cloud),
the record must be DNS-only — proxied records drop raw TCP/UDP traffic.

## Default configuration

The router starts as a **floodfill** volunteer (it stores and serves the network's
destination database). This is optional public service — to run as a plain relay
instead, uncheck floodfill under *Config → Router manager* and reboot the router
from the console.

Bandwidth limits are also set under *Config → Router manager*.

## Do not

- **Do not use the console's "update now"** — the router's self-updater is
  disabled on purpose; updates arrive via `yunohost app upgrade i2p`.
- The console listens on loopback only; it is reachable exclusively through the
  SSO-gated proxy. Keep it that way.

Further administration, settings, and troubleshooting: see the app's
**Documentation** tab (admin doc) in the YunoHost admin.
