---
title: "ssh"
weight: 531
pre: <b>3.1.5.3.1 </b>
---

{{% notice warning %}}
ZGrab2 integration is experimental and porting is currently not complete.
[You can help adding modules and improve stability.]({{< ref "/contribute" >}})
{{% /notice %}}

#### `subscribePorts: ["tcp/22"]`

Ports to subscribe. If one of these is found open, this scanner module is triggered against that target.

#### `timeout: 2500ms`

Timeout before the scan is cancelled.

#### `ClientID: "SSH-2.0-Go"`

SSH client ID to present to the server.

#### `CollectUserAuth: true`

If set to true, possible client authentication options are queried.
