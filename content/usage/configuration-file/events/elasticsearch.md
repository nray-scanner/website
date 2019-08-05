---
title: "elasticsearch"
weight: 630
pre: <b>3.1.6.3 </b>
---

#### `enabled: false`

Enables the elasticsearch event handler. If true, all events are also sent to elasticsearch. This is useful for performing queries or visualizing data, e.g. using Kibana.

#### `server: "elasticsearch.local"`

The name or IP address of the elasticsearch node.

#### `useTLS: true`

Forces use of TLS.

#### `port: 443`

TCP port elasticsearch is listening on.

#### `internal.indexname: "nray-scanner"`

The name of the index.

#### `internal.channelsize: 10000`

Size of the internal buffer holding events between commits.
      
#### `internal.committimer: 3`

Interval to commit data.