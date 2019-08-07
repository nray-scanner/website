---
title: "certificatetransparency"
weight: 6
pre: <b>3.1.4.2 </b>
---

The `certificatetransparency` streams data from [certstream](https://certstream.calidog.io/), a certificate transparency log stream. This allows to inspect all publicly issued certificates. Using this data, port scans may be issued against targets right after they obtain a certificate, usually during setup before any hardening or default password changes have been in place.

{{% notice tip %}}
This may come in handy for bug bounties - if this turns out to be the new bounty hunter's cash cow, the nray authors would love to receive a small tip for their voluntary work <i class="far fa-smile-wink"></i> 
{{% /notice %}}

#### `enabled: false`

Enables or disables this target generator.

#### `domainRegex: '^.*$'`

Scan every site that obtains a certificate and matches the pattern `www.somethingsomething.com`. 
The default matches every domain name, to match for example `www.somethingsomething.com` an expression like `^(www[.]).*([.]com)$` may be used.
Since regex becomes tricky fast, [this play](https://play.golang.org/p/jgDiTmPlqdW) can be adopted to see if the expression works as intended.

{{%expand "Code to try your own regular expression against a domain" %}}
~~~golang
package main

import (
	"fmt"
	"regexp"
)

var regex = "^(www[.]).*([.]com)$"
var toCheck = "www.google.com"

func main() {
	re := regexp.MustCompile(regex)
	fmt.Println(re.MatchString(toCheck))
}
~~~
{{% /expand%}}

Interesting use case ideas: Scan `mail.*` for open relays on port 25, check new `jenkins.*` instances if `/script` endpoint is present, or maybe there is some software out there that still uses default passwords? Endless possibilities!

#### `tcpports: ["top25"]`

List of TCP ports to scan. Supports enumerations (`[20,21,22,23]`), ranges (`[8000-8100]`) or nmap-style top-lists (e.g. `["top50"]`). 
You may also mix, e.g. `[20,21,22,23,8000-8100,"top50"]`. 
Duplicates are filtered out <i class="far fa-smile-wink"></i>

#### `udpports: [top25]`

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

#### `maxHostsPerBatch: 150`

Specifies how many target hosts are contained in a single work batch sent to a node. The higher the number, the more hosts have to be scanned by a single node before fetching new work. Should be tweaked together with `maxTcpPortsPerBatch` and `maxUdpPortsPerBatch` as well as depending on the actual requirements. You may take a look at [A note on work scheduling](../#a-note-on-work-scheduling).

#### `maxTcpPortsPerBatch: 25`

Specifies how many TCP ports are scheduled for a single work batch. The higher the number, the more TCP ports are scanned (if requested) before fetching new work. Should be tweaked together with `maxHostsPerBatch` and `maxUdpPortsPerBatch` as well as depending on the actual requirements. You may take a look at [A note on work scheduling](../#a-note-on-work-scheduling).


#### `maxUdpPortsPerBatch: 25`

Specifies how many UDP ports are scheduled for a single work batch. The higher the number, the more UDP ports are scanned (if requested) before fetching new work. Should be tweaked together with `maxHostsPerBatch` and `maxTcpPortsPerBatch` as well as depending on the actual requirements. You may take a look at [A note on work scheduling](../#a-note-on-work-scheduling).