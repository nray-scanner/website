---
title: "http"
weight: 532
pre: <b>3.1.5.3.2 </b>
---

{{% notice warning %}}
ZGrab2 integration is experimental and porting is currently not complete.
[You can help adding modules and improve stability.]({{< ref "/contribute" >}})
{{% /notice %}}

{{% notice info %}}
The naming of this module's subscription parameters differ from other ZGrab2 modules due to the need to differentiate between HTTP and HTTPS.
{{% /notice %}}

#### `subscribeHTTPPorts: ["tcp/80", "tcp/8080", "tcp/8000"]`

Ports to subscribe for HTTP scanning. If one of these is found open, the HTTP scanner module is triggered against that target.

#### `subscribeHTTPSPorts: ["tcp/443", "tcp/8443"]`

Ports to subscribe for HTTPS scanning. If one of these is found open, the HTTPS scanner module is triggered against that target.

#### `timeout: 2500ms`

Timeout before the scan is cancelled.

#### `method: "GET"`

HTTP method to use.

#### `endpoint: "/"`

HTTP endpoint to request.

#### `userAgent: "nray"`

User Agent to send with the HTTP requests.

#### `retryHTTPS: true`

In case a HTTP connection fails, HTTPS is tried if this option is set to true.

#### `maxRedirects: 2`

How many redirects to follow before giving up.
