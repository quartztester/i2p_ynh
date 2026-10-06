The I2P router console is available at **https://\_\_domain\_\_/** — it is gated behind YunoHost's SSO, so only users of your portal can reach it.

**One last step for good citizenship:** forward port **\_\_port\_ext\_\_ (TCP *and* UDP)** on your internet box/router to this server. Check the console's status page: it should say **Network: OK**. If it says **Firewalled**, the port forward is missing or wrong, and the relay contributes much less.

The router is running as a **floodfill** volunteer by default. Everything (including that) is configurable inside the console under *Config → Router manager*.
