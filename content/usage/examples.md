---
title: "Examples"
weight: 500
pre: <b>3.5 </b>
---

This page contains some examples to get your nray experience started quickly.

All examples assume that the binary is called `nray`, of course you have to adapt this to the name of your binary.

### Simple port scan from local machine

{{% notice warning %}}
Unfortunately, due to a bug in the upstream project of the configuration parser, currently some options mustn't be omitted. See [this issue](https://github.com/nray-scanner/nray/issues/6) for more information. The following configuration has therefore all options listed, albeit most of them are disabled. The relevant settings are marked with a comment.
{{% /notice %}}

- Edit the configuration file (e.g. `config.yaml`) to contain the following:

~~~yaml
debug: false 
listen: [8601] # Port to listen
host: "127.0.0.1" # host to listen (only localhost)
pools: 1 # Only use a single pool

TLS:
  enabled: false
  CA: "/path/to/ca.pem"
  cert: "/path/to/servercert.pem"
  key: "/path/to/servercert-key.pem"
  forceClientAuth: false

considerClientPoolPreference: true
allowMultipleNodesPerHost: false
internal:
  nodeExpiryTime: 30
  nodeExpiryCheckInterval: 10

targetgenerator:
  bufferSize: 5
  standard:
    enabled: true
    targets: ["192.168.178.1/28"] # target network to scan
    tcpports: ["top25"] # which TCP ports to scan
    udpports: [] # don't scan UDP
    blacklist: [] # no blacklist
    maxHostsPerBatch: 20
    maxTcpPortsPerBatch: 25
    maxUdpPortsPerBatch: 25
  certificatetransparency:
    enabled: false
    domainRegex: '^(www[.]).*([.]com)$'
    tcpports: [top25]
    udpports: [top25]
    blacklist: []
    maxHostsPerBatch: 150
    maxTcpPortsPerBatch: 25
    maxUdpPortsPerBatch: 25
  ldap:
    enabled: false
    ldapSearchString: "(objectCategory=computer)"
    baseDN: "dc=contoso,dc=com"
    ldapAttribute: "dNSHostName"
    ldapServer: ""
    ldapPort: 636
    insecure: false
    ldapUser: ""
    ldapPass: ""
    tcpports: [top25]
    udpports: [top25]
    blacklist: []
    maxHostsPerBatch: 5
    maxTcpPortsPerBatch: 25
    maxUdpPortsPerBatch: 25
scannerconfig:
  workers: 250 # Run with 250 workers
  ratelimit: "none" # No rate limit
  tcp:
    timeout: 2500ms # 2.5s TCP timeout
  udp:
    fast: false
    defaultHexPayload: "\x6e\x72\x61\x79"
    timeout: 2500ms
  zgrab2:
    enabledModules: []
    ssh:
      subscribePorts: ["tcp/22"]
      timeout: 2500ms
      ClientID: "SSH-2.0-Go-nray" 
      CollectUserAuth: true
    http:
      subscribeHTTPPorts: ["tcp/80", "tcp/8080", "tcp/8000"]
      subscribeHTTPSPorts: ["tcp/443", "tcp/8443"]
      timeout: 2500ms
      method: "GET"
      endpoint: "/"
      userAgent: "nray" 
      retryHTTPS: true 
      maxRedirects: 2
events:
  terminal:
    enabled: true # print events to terminal
    internal:
      channelsize: 1000
  json-file: 
    enabled: true # write events to file
    filename: "nray-output.json" # filename
    overwriteExisting: false 
    internal:
      channelsize: 10000 
      synctimer: 10s
  elasticsearch:
    enabled: false
    server: "elasticsearch.local"
    useTLS: true
    port: 443
    internal:
      indexname: "nray"
      channelsize: 10000
      committimer: 3
~~~

- Next, run the server: `./nray server -c /path/to/config.yaml`. 
- Finally, run a node on the same system: `./nray node`. If no server and port is specified, nodes always try to connect to localhost:8601 whereas other values can be injected at compile time or can be passed via `-s <server>` and `-p <port>` parameter.
- If there are systems in the network having ports opened, you should now see events for each port found.
- Results are also written to `nray-output.json`

### jq library

[jq](https://stedolan.github.io/jq/) is an excellent command line JSON processor. 
It allows to view and query JSON documents and you may give it a shot for accessing the event file.

{{% notice tip %}}
For live viewing, `jq -C '<expr>' <outputfile> | less -R` gives you scrollable, colorized output. During a scan, you can also `tail -f <outputfile> | jq '<expr>'`.
{{% /notice %}}

Here are some example queries to get you started:

#### Show all events where port 22 was involved

~~~bash
jq '. | select(.result.port == 22)' <outputfile>
~~~

This includes TCP, UDP and ZGrab2 events.

#### Show all events where tcp port 80 was found open

~~~bash
jq '. | select(.result.portscan.port == 80 and .result.portscan.open == true and .result.portscan.scantype == "tcpconnect")' <outputfile>
~~~

Actually, the `result.portscan.open` can be omitted since closed ports do not generate events.

#### Show only IPs/names of systems where tcp port 80 was found open

~~~bash
jq '. | select(.result.portscan.port == 80 and .result.portscan.open == true and .result.portscan.scantype == "tcpconnect") | .result.target' <outputfile>
~~~

