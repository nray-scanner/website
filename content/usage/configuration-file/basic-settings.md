---
title: "Basic settings"
weight: 100
pre: <b>3.1.1 </b>
---

### Top level configuration options

#### `debug: false`

Enables debug output *serverside*. 

#### `listen: [8601]`

The port to listen on. Multiple ports may be specified, e.g. `listen: [22, 80, 443, 3389]` to listen on ports 22, 80, 443 and 3389. This may make it easier for you to operate a server with nodes in different networks and firewall policies.

#### `host: "127.0.0.1"`

The address to listen on. `"0.0.0.0"` listens on all interfaces. IPv6 may work, too, but this is has not been tested yet.

#### `pools: 1`

Configures the number of pools. Please refer to [pooling](../pooling) for more information.

#### `considerClientPoolPreference: true`

Clients may request to be placed in a specific pool. This is required when nodes in a pool share specific properties, e.g. all nodes inside the same pool are in the same country.