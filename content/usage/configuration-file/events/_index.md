---
title: "events"
weight: 600
pre: <b>3.1.6.0 </b>
---

### Filtering

All event handlers support filtering of events. 
This is especially useful if particular events are of special interest, e.g. specific open ports.

The configuration option to enable filtering for an event handler is called `filter` and has the name of the JSON fields as options.

The following example example of the terminal filter prints all events of type `environment` or where `portscan.port` is 25:

~~~yaml
events:
  terminal:
    enabled: true
    # Any matching filter is going to be printed
    filter: 
      environment: # empty filter is printed if a element of this type exists
      result.port: 25 # All port 25 events, regardless of scanning module. 
    internal:
      channelsize: 1000
~~~

In this case, this is only applied to the terminal event handler - but filtering works the same way for other event handlers, too.