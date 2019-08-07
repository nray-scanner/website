---
title: "Command line flags (node)"
weight: 200
pre: <b>3.2 </b>
---

Because nodes are going to deployed in a variety of scenarios in different environments, providing a configuration file is not viable.
Most options are configured server side and transmitted when the node connects first, but at least the location and and connection settings (like TLS configuration) are required when a node is started.

The following options apply when nray runs as node (`nray node`):

#### `--debug`

Enable debug output.

#### `-h, --help`

Print a help message.

#### `--node-name <name>`

Assign a name to this scanning node. Useful if you are running multiple nodes and want to distinguish results in the event logs.

#### `-p, --port <port number> `

Nray server port. Usually 8601.

#### `--preferred-pool <pool number>`

Pool to be preferably placed in at the server. If configured, the server respects this as long as the pool exists.

#### `-s, --server <server address or name>`

Nray server address.

#### `--tls-ca-cert <path>`       

Path to ca certificate if TLS is used. Requires `--use-tls`.

#### `--tls-client-cert <path>`   

Path to tls client cert. Requires `--use-tls`.

#### `--tls-client-key <path>`    

Path to tls client key. Requires `--use-tls`.

#### `--tls-insecure`             

Literally. Trust anybody. Don't do this in networks you do not fully trust. Requires `--use-tls`.

#### `--tls-server-SAN <subject alternative name of server>`    

Subject alternative name of the server. Go's TLS implementation checks this value against the values provided in the certificate and refuses to connect if no match is found.

#### `--use-tls`

Set true to use TLS.
