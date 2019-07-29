---
title: "targetgenerator"
weight: 420
pre: <b>3.1.4.0 </b>
---

Everything that produces a stream of targets that need to be scanned is a target generator.
Due to the modular design, it should be easy to implement your own generators from your data sources.

#### `bufferSize: 5`

Size of the work batch buffer. If you are planning to have a lot of nodes or a lossy data input stream, you may increase this number, otherwise it simply consumes a little bit more memory.


### A note on work scheduling

Understanding how nray schedules work may allow you to greatly improve performance. In order to explain the inner workings in greater detail, take a look at following configuration of the standard target generator:

~~~yaml
targets: ["10.0.0.0/22"]
tcpports: ["top500"]
udpports: [""]
maxHostsPerBatch: 150
maxTcpPortsPerBatch: 25
~~~

In this case, the network consists of about 1000 hosts to scan for the 500 most common TCP ports. In order to distribute this task across nodes, nray chops it into pieces, so called *work batches* that are requested and processed by nodes. In this case, each batch is going to contain a list of 150 hosts and 25 TCP ports that have to be scanned on these hosts. In order to scan all hosts, 7 batches would be enough, but there is also the port restriction. Each batch must not contain more than 25 ports, therefore 20 batches are required to scan all TCP ports for a single host group. In the end, `7 * 20 = 140` batches are created for the above configuration.

In case for example only ports 22, 80 and 443 are of interest, you may scale up `maxHostsPerBatch` whereas if you only want to scan a few hosts but on a large number of ports, you may advise nray to create batches containing only one or two hosts, but for example 10000 ports.

A good rule of thumb is to find a configuration such that nodes call back for more work every ~15-20 seconds - this gives you results often and fast and in case a node gets lost, fewer work has to be rescheduled.