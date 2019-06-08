---
title: "Installation"
date: 2019-04-07T00:17:57+02:00
weight: 20
pre: <b>2. </b>
---

Nray is written in Go and care was taken to select only dependencies that also fulfill this requirement.
This allows to build *completely static* binaries that do not require any runtime dependencies.
Furthermore, nray is designed for running as unprivileged user. 
Since Go supports a wide range of [operating systems and architectures](https://github.com/golang/go/blob/master/src/go/build/syslist.go), it is possible to run nray on nearly any system with least user rights - the perfect solution to gain insight even into highly separated networks.

To sum it up: It is not required to install nray and it is supposed to run *anywhere*. Just drop and run the binary! There are [prebuilt releases](prebuilt) as well as instructions on [building your own](build-your-own).

Once you obtained a binary for your environment, take a look at the [usage section](../usage).