---
title: "targetgenerator"
weight: 4
pre: <b>3.1.4 </b>
---

Everything that produces a stream of targets that need to be scanned is a target generator.
Due to the modular design, it should be easy to implement your own generators from your data sources.

#### `bufferSize: 5`

Size of the work batch buffer. If you are planning to have a lot of nodes or a lossy data input stream, you may increase this number, otherwise it simply consumes a little bit more memory.
