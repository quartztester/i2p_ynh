I2P (Invisible Internet Project) is a global, decentralized overlay network for anonymous communication. Traffic is relayed through encrypted, single-hop tunnels that pass through other volunteers' routers before reaching its destination, making it hard to observe who is talking to whom.

This package runs a full I2P router that participates in the network as a relay: it forwards other users' traffic and helps maintain the network's routing database (and may be promoted to a "floodfill" directory node). The router console (statistics, peer and tunnel info, log level) is served on its own domain behind YunoHost's SSO — anonymous visitors cannot reach it.

Nothing is proxied for website visitors; the router only shuttles encrypted I2P traffic, the same as every other I2P node on the network. See the README for ISP/terms-of-service considerations before volunteering bandwidth.
