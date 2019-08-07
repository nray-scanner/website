---
title: "ldap"
weight: 7
pre: <b>3.1.4.3 </b>
---

The `ldap` target generator allows to connect to a ldap server in order to identify scan targets. Especially in Active Directory environments this is really useful since computer objects have a `dNSHostName` property and Donmain Controllers usually act also as DNS servers [that can be queried via LDAP](https://dirkjanm.io/getting-in-the-zone-dumping-active-directory-dns-with-adidnsdump/).

#### `enabled: false`

Enables or disables this target generator.

#### `ldapSearchString: "(objectCategory=computer)"`

The ldap search to perform for selecting objects. In Active Directory environments, `(objectCategory=computer)` can be used to select all computer objects.

#### `baseDN: "dc=contoso,dc=com"`

Base DN to start search.

#### `ldapAttribute: "dNSHostName"`

On all selected objects, extract `ldapAttribute`. This one is going to be scanned. In Active Directory envrionments, chances are that `dNSHostName` can be resolved and is alive.

#### `ldapServer: ""`

The ldapServer to connect to.

#### `ldapPort: 636`

The ldap port. Usually 636 for encrypted connections and 389 for unencrypted.

#### `insecure: false`

Don't use TLS.

#### `ldapUser: ""`

Username to perform the ldap bind. For Active Directory domains, `<user>@<domain.fqdn>`.

#### `ldapPass: ""`

The user's password.

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

#### `maxHostsPerBatch: 150`

Specifies how many target hosts are contained in a single work batch sent to a node. The higher the number, the more hosts have to be scanned by a single node before fetching new work. Should be tweaked together with `maxTcpPortsPerBatch` and `maxUdpPortsPerBatch` as well as depending on the actual requirements. You may take a look at [A note on work scheduling](../#a-note-on-work-scheduling).

#### `maxTcpPortsPerBatch: 25`

Specifies how many TCP ports are scheduled for a single work batch. The higher the number, the more TCP ports are scanned (if requested) before fetching new work. Should be tweaked together with `maxHostsPerBatch` and `maxUdpPortsPerBatch` as well as depending on the actual requirements. You may take a look at [A note on work scheduling](../#a-note-on-work-scheduling).


#### `maxUdpPortsPerBatch: 25`

Specifies how many UDP ports are scheduled for a single work batch. The higher the number, the more UDP ports are scanned (if requested) before fetching new work. Should be tweaked together with `maxHostsPerBatch` and `maxTcpPortsPerBatch` as well as depending on the actual requirements. You may take a look at [A note on work scheduling](../#a-note-on-work-scheduling).