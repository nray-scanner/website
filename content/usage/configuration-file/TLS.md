---
title: "TLS"
weight: 2
pre: <b>3.1.2 </b>
---

### TLS

{{% notice warning %}}
If you are running nray in any other than your home network, make sure to enable TLS or you are going to have a bad time! If you don't know what TLS is or don't have a basic understanding of how these parameters play together, you should not run nray over untrusted networks!
{{% /notice %}}

Nray relies on Golang, more specifically [mangos](https://github.com/nanomsg/mangos), to provide support for TLS 1.2. TLS works with key material created by following the instructions of the [TLS quick start guide](../guides/tls-quick-start) TODO.


#### `enabled: false`

Enables TLS. 
When operating nray over untrusted networks (like the Internet!), it is highly advised to protect the confidentially and integrity of the communication with nodes.
Nray supports use of TLS 1.2, also with mutual authentication if required.

#### `CA: ""`

Path to the CA certificate.

#### `cert: ""`

Path to the server certificate.

#### `key: ""`

Path to the server certificate private key.

#### `forceClientAuth: false`

If true, clients have to authenticate themselves with a certificate issued by a (sub-)CA. 