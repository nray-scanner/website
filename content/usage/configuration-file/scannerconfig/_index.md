---
title: "scannerconfig"
weight: 500
pre: <b>3.1.5.0 </b>
---

#### `workers: 250`

How many asynchronous workers to spawn. 
There are operating system restrictions to the number of open file descriptors of a process, e.g. 1024 on most modern Linux distributions.
Since some of them are required for internal usage (e.g. communication with server), from experience 1000 is pretty much the best you may get on x64_linux whereas different limits may apply on other operating systems / architectues. 
  
#### `ratelimit: "none"`

A rate limit can be set to control how many workers start their scan within a second. This becomes handy to avoid bursts with many workers where scans have long durations / timeouts, e.g. a scan having a timeout of 10 seconds with 1000 workers may be throttled to 100 workers starting their scan each second (instead of all at the beginning) by setting `ratelimit: 100`.