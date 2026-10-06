# I2P router — YunoHost package

Run a volunteer I2P router (relay + netdb participant) on a YunoHost server.
Strengthens the I2P anonymous network. Nothing on your server is proxied for
visitors; the router only forwards other users' traffic, as every I2P node does.

## What it does

- Runs the official [`geti2p/i2p`](https://github.com/i2p/i2p.i2p/blob/master/Docker.md)
  Docker image behind systemd (relay-only; client apps stay loopback-bound).
- Opens one peer port (TCP+UDP, default `51427`) and adds the SSO portal tile.
- The router console (stats, network, log level) is served on a dedicated domain
  behind YunoHost SSO — no anonymous access, no second login.

## Requirements

- YunoHost ≥ 12
- Docker (`apt install docker.io docker-compose-v2`)
- A **dedicated (sub)domain** — e.g. `i2p.example.com`. The console UI uses
  absolute URLs, so paths other than `/` are refused.
- **Router port-forwarding**: forward TCP *and* UDP on the chosen external port
  to this server's LAN address. Without it the router shows "Firewalled" and
  contributes almost nothing.

## Install

```bash
yunohost app install https://path/to/this/repo \
  -a "domain=i2p.example.com&path=/&ext_port=51427&jvm_xmx=512m"
```

## Console

`https://your-domain/` (SSO-gated). The router's `routerconsole.allowedHosts`
is managed automatically on install/upgrade/`change-url`.

## Notes

- `jvm_xmx`: max JVM heap (default 512m). If the container restarts with
  `OutOfMemoryError`, raise to 768m/1024m and `yunohost app upgrade`.
- Peer traffic is outbound-first; consider this a public service. On residential
  ISPs, review your terms before volunteering (floodfill = even more exposure).
- Router identity lives in the `i2p-data` docker volume — losing it means a new
  router hash.
- `yunohost app change-url i2p -d new.example.com` is supported (root path only).
