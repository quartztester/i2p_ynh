**Before installing, two things to know:**

- This app **volunteers your server's bandwidth** to the I2P anonymous network. By default the router registers as a *floodfill* — one of the directory servers that answer routing-database queries for the whole network. Expect a steady trickle of traffic from strangers (typically a few hundred kB/s). Nothing readable passes through: all I2P traffic is end-to-end encrypted, exactly like a Tor relay. Still, check that your ISP's terms of service tolerate relay traffic before proceeding.
- The router needs its peer port (default **51427, TCP *and* UDP**) forwarded on your home router/box to this server, or it will run "Firewalled" and be of little use to the network. You can set this up after the install.
