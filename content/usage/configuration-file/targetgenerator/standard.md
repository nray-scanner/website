---
title: "standard"
weight: 5
pre: <b>3.1.5 </b>
---

This is the standard target generator that is probably going to be used most of the time. 
It takes a list of IPs, CIDR networks or domain names as targets and black list as well as a list of TCP and UDP ports to be scanned.

#### `enabled: true`

Enables or disables this target generator.

#### `targets: ["192.168.178.1/28"]`

A list of targets to scan. 
May be CIDR networks, IPs or domain names.

#### `targetFile: ""`

A file containing a list of targets to scan. 
May be CIDR networks, IPs or domain names, newline separated.

#### `tcpports: ["top50"]`

List of TCP ports to scan. Supports enumerations (`[20,21,22,23]`), ranges (`[8000-8100]`) or nmap-style top-lists (e.g. `["top50"]`). 
You may also mix, e.g. `[20,21,22,23,8000-8100,"top50"]`. 
Duplicates are filtered out <i class="far fa-smile-wink"></i>

#### `udpports: []`

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


#### `maxTcpPortsPerBatch: 25`


#### `maxUdpPortsPerBatch: 25`