---
title: "Pooling"
weight: 300
pre: <b>3.3 </b>
---

The core concept around nray's work distribution functionality is pooling.

Nray internally has a list of pools, how many can be specified via the `pools: n` directive in the configuration file.
The idea is that each pool performs a scan of all targets, which means that each pool creates a complete view.
Each pool may contain an arbitrary number of scanner nodes that work together on performing the scan.

This means that speeding up a scan by bringing more workers in is achieved by placing them all in the same pool whereas creation of network views is done by creating a pool for each desired view.

In it's default configuration, nray only has a single pool and currently pools don't support names, so they are numbered starting with 0.
In case multiple pools are available, nray is going to place new nodes in the pool with fewest members. 
In order to manually control which pool a node should be assigned to, set `considerClientPoolPreference: true` in the nray configuration and start the nodes with `--preferred-pool x`. For example, if you want to connect a node to a server and place it into pool 2, you may run the following command: `nray node -s <server ip> -p <server port> --preferred-pool 2`.