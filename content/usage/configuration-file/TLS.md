---
title: "Internal"
weight: 3
pre: <b>3.1.3 </b>
---

### internal

{{% notice warning %}}
Everything called **internal** is... well internal and you should only change it if you know what you are doing. This also applies to internal objects exposed by other configuration nodes.
{{% /notice %}}

#### `nodeExpiryTime: 30s`

Timeout to expire nodes that did not send heart beats.

#### `nodeExpiryCheckInterval: 10s`

How often to check for expired nodes.