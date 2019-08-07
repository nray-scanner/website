---
title: "json-file"
weight: 620
pre: <b>3.1.6.2 </b>
---

#### `enabled: true`

Enables logging of events to a file. 

#### `filename: "nray-output.json"`

The filename to log to.

#### `overwriteExisting: false`

If set to `false`, this option prevents from (accidentally) overwriting existing output files. 

#### `internal.channelsize: 10000`

Size of the internal buffer holding events between force flushing to file system.

#### `internal.synctimer: 10s`

Interval to flush data to the file system.