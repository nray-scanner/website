---
title: "zgrab2"
weight: 530
pre: <b>3.1.5.3 </b>
---

{{% notice warning %}}
ZGrab2 integration is experimental and porting is currently not complete.
[You can help adding modules and improve stability.]({{< ref "/contribute" >}})
{{% /notice %}}

[ZGrab2](https://github.com/zmap/zgrab2) is an awesome application layer scanner. Since it is supposed to run standalone and doesn't provide an API, integration into nray requires some glue code for each module to work.

Nray's ZGrab2 integration uses a subscription-based approach for performing application layer scans.
Suppose the following configuration:

~~~yaml
ssh:
    subscribePorts: ["tcp/22", "tcp/222", "tcp/2222"]
    timeout: 2500ms
~~~

Here, an SSH application layer scan with its own timeout of 2500ms is triggered every time an open port `tcp/22`, `tcp/222`, or `tcp/2222` is found.

Nray's ZGrab2 integration runs also concurrent to other scans, using the worker pools and rate limits assigned in the [scanner configuration](../).
The result produced are also in JSON format and fit into the events produced by nray's port scanning functionality.

#### `enabledModules: ["ssh", "http"]`

Which ZGrab2 modules to enable. Currently, the following modules are supported:

- SSH
- HTTP (includes HTTPs and various TLS checks)