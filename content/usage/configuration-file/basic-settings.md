---
title: "Basic settings"
weight: 100
pre: <b>3.1.1 </b>
---

### Top level configuration options

#### `debug: false`

Enables debug output *server side*. 

#### `listen: [8601]`

The port to listen on. Multiple ports may be specified, e.g. `listen: [22, 80, 443, 3389]` to listen on ports 22, 80, 443 and 3389. This may make it easier for you to operate a server with nodes in different networks and firewall policies.

#### `host: "127.0.0.1"`

The address to listen on. `"0.0.0.0"` listens on all interfaces whereas `"127.0.0.1"` only listens on the loopback interface. IPv6 may work, too, but this is has not been tested yet.

#### `pools: 1`

Configures the number of pools. Please refer to [pooling](../pooling) for more information.

#### `considerClientPoolPreference: true`

Clients may request to be placed in a specific pool. This is required when nodes in a pool share specific properties, e.g. all nodes inside the same pool are in the same country.

#### `allowMultipleNodesPerHost: false`

This randomizes the nodeID, allowing to run multiple nodes on the same machine or in scenarios where no unique ID can be generated from the environment, for example container environments like Kubernetes.
This is disabled by default because it is inconsistent with the environment information transmitted during node registration and makes it impossible to find out which node generated an event in the current implementation.
Enabling this option does not break functionality and if nray is used on a single system or container cluster, the system that generated a specific event is probably of no interest. 
In scenarios where nray runs on a heterogeneous fleet, it may be relevant to track which system generated an event afterwards, so make sure to have this option disabled in those scenarios.