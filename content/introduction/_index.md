---
title: "Introduction"
weight: 100
pre: <b>1. </b>
---

Nray is a sophisticated port scanner **built from scratch**. No Nmap wrappers, no Python glue code, no weekend project.

Nray doesn't require administrative permissions and runs dependencyless on nearly any architecture and operating system. 
Nevertheless, its scan speed is superior to Nmap in most cases while delivering nearly the same result quality regarding discovered ports.

Apart from that, nray introduces fresh ideas when it comes to target selection and result processing:

- Target selection:
  - IP, domain names and network lists - the usual stuff.
  - Nray allows to observe the [certificate transparency](https://en.wikipedia.org/wiki/Certificate_Transparency) log and extract domain names from certificates issued nearly in real time.
  - Nray can connect to LDAP (e.g. Active Directory) and perform arbitrary queries, e.g. obtain all registered computer objects and extract their FQDNs.
  - DNS zone transfer planned.
- Output
  - An event stream encoded as JSON data allows to search and use the results while the scan is still running.
  - Native elasticsearch integration: Scan results are stored in your elasticsearch cluster as they arive. Easily search and analyze the results of your network scans to gain valuable high-level insights.
  - Splunk and metasploit planned.
- Modularity: Want to integrate your CMDB or network inventory to nray? You prefer .csv output because it opens in Excel? Target selection and event processing is built in a modular way, therefore it should not be too hard for you to adapt nray to your requirements.

Nray allows to perform application layer scans for selected protocols, e.g. SSH or HTTP, using the [ZGrab2 framework](https://github.com/zmap/zgrab2). 
The results are, of course, fully integrated into the event-based JSON result stream.

As mentioned, nray is designed as distributed network scanner. 
The server-client model allows to spin up an arbitrary number of *nodes* that perform a scan orchestrated by a *server*.
This allows to scale scan speed linearly by introducing more nodes or to create network views by scanning from different vantage points.

Sounds too good? [Give it a shot!](../installation/)