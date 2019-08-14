---
title: "udp"
weight: 520
pre: <b>3.1.5.2 </b>
---


#### `fast: false`

Fast sends only known payloads to known ports. The list and payloads are taken from the Metasploit project and it contains currently UDP ports 1604, 53, 137, 123, 524, 5093, 1434, 161, and 111.

#### `defaultHexPayload: "\x6e\x72\x61\x79"`

Since UDP is connection-less, a payload needs to be sent. 
This option configures the default payload that is sent if no custom payload is specified for a port.
ASCII is supported as well as hexadecimal and octal data representation.
`\x6e\x72\x61\x79` is hexadecimal for `nray`.

#### `customHexPayloads: `

Allows to specify custom payloads for specific ports. The example below sends a single `'A'` character to udp/19:

~~~yaml
customHexPayloads: 
  "19": "A" # chargen. "A" is the same as "\x41" (hex) or "\101" (oct)
~~~

#### `timeout: 2500ms`

Timeout for UDP. If no response is received within this time frame, a port is marked closed.