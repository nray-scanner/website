---
title: "standard"
weight: 5
pre: <b>3.1.4.1 </b>
---

This is the standard target generator that is probably going to be used most of the time. 
It takes a list of IPs, CIDR networks or domain names as targets and black list as well as a list of TCP and UDP ports to be scanned.

#### `enabled: true`

Enables or disables this target generator.

#### `targets: []`

A list of targets to scan. 
May be (also a mix of) CIDR networks, IPs or domain names.

Example:

~~~yaml
standard:
    enabled: true
    targets: ["192.168.1.1/24", "192.168.16.0/22", "somesystem.domain.local", "192.168.12.14"]
    tcpports: ["top25"]
    udpports: ["top25"]
    maxHostsPerBatch: 150
    maxTcpPortsPerBatch: 25
    maxUdpPortsPerBatch: 25
~~~

#### `targetFile: ""`

A file containing a list of targets to scan. 
May be CIDR networks, IPs or domain names, newline separated.

#### `tcpports: ["top25"]`

List of TCP ports to scan. Supports enumerations (`[20,21,22,23]`), ranges (`[8000-8100]`) or nmap-style top-lists (e.g. `["top50"]`). 
You may also mix, e.g. `[20,21,22,23,8000-8100,"top50"]`. 
Duplicates are filtered out <i class="far fa-smile-wink"></i>

#### `udpports: ["top25"]`

List of UDP ports to scan. Supports enumerations (`[20,21,22,23]`), ranges (`[8000-8100]`) or nmap-style top-lists (e.g. `["top50"]`). 
You may also mix, e.g. `[20,21,22,23,8000-8100,"top50"]`. 
Duplicates are filtered out <i class="far fa-smile-wink"></i>

#### `blacklist: []`

A list of targets not to scan. 
May be CIDR networks, IPs or domain names.

{{% notice info %}}
DNS resolution happens at the node and there is no reverse DNS lookup. 
This has important implications.
For example, consider *example.local* resolving to *10.10.10.10*. 
When blacklisting *example.local* but scanning for *10.10.10.0/24*, the server is going to be scanned. When blacklisting *10.10.10.0/24* but scanning for *example.local*, the server is going to be scanned.
{{% /notice %}}

#### `blacklistFile: "./blacklist.txt"`

A file containing a list of targets to scan. 
May be CIDR networks, IPs or domain names, newline separated.

{{% notice info %}}
DNS resolution happens at the node and there is no reverse DNS lookup. 
This has important implications.
For example, consider *example.local* resolving to *10.10.10.10*. 
When blacklisting *example.local* but scanning for *10.10.10.0/24*, the server is going to be scanned. When blacklisting *10.10.10.0/24* but scanning for *example.local*, the server is going to be scanned.
{{% /notice %}}

#### `maxHostsPerBatch: 150`

Specifies how many target hosts are contained in a single work batch sent to a node. The higher the number, the more hosts have to be scanned by a single node before fetching new work. Should be tweaked together with `maxTcpPortsPerBatch` and `maxUdpPortsPerBatch` as well as depending on the actual requirements. You may take a look at [A note on work scheduling](../#a-note-on-work-scheduling).

#### `maxTcpPortsPerBatch: 25`

Specifies how many TCP ports are scheduled for a single work batch. The higher the number, the more TCP ports are scanned (if requested) before fetching new work. Should be tweaked together with `maxHostsPerBatch` and `maxUdpPortsPerBatch` as well as depending on the actual requirements. You may take a look at [A note on work scheduling](../#a-note-on-work-scheduling).


#### `maxUdpPortsPerBatch: 25`

Specifies how many UDP ports are scheduled for a single work batch. The higher the number, the more UDP ports are scanned (if requested) before fetching new work. Should be tweaked together with `maxHostsPerBatch` and `maxTcpPortsPerBatch` as well as depending on the actual requirements. You may take a look at [A note on work scheduling](../#a-note-on-work-scheduling).