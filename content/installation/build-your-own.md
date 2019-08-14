---
title: "Build Your Own"
weight: 250
---

Want to build your own? Great, that's the spirit! If you know git and command line basics, it isn't too hard, promised! <i class="far fa-smile-beam"></i>

#### Quick and easy

1. First, you need [git](https://git-scm.com/) and [Go](https://golang.org/) installed. Once they are in place, clone the [nray repository](https://github.com/nray-scanner/nray) and check out the desired branch. Official releases are built from `master` whereas the hot new stuff is located in `develop` or feature branches.
2. Open a terminal, navigate to the checked out folder and run `go get -u` followed by `go build` 
3. **That's it!** You just built a nray binary for your system without any obvious magic involved!

#### Taking a closer look

Usually it is easy to build a binary that runs on the current system, therefore this is no unique selling point. Go's ability to generate binaries for most operating systems and architecture without requiring third party libraries (like glibc!) as well as the excellent cross-compiling capabilities were a main reason for choosing this language. It also supports injecting values for variables at compile time which comes in handy in some situations.

In order to understand what is going on, we are going to look at an excerpt of the actual Makefile. Fear not, this is not the kind of complex Makefile you may have seen in the past as the build process for nray is quite simple and straight-forward.

In this example, we are going to look at the (slightly simplified) `build-armv7-linux` and `build-localarch` targets:

~~~make
build-armv7-linux:
	CGO_ENABLED=0 GOOS=linux GOARCH=arm GOARM=7 go build -ldflags "-s -w" -o build/nray-armv7-linux ./nray.go 
~~~

- `CGO_ENABLED=0`: Disables CGO, in other words: Make sure no C-code is used or linked. On some platforms, the Go-compiler may prefer existing C code for some functionality which decreases portability. We explicitly disable this behavior to make sure the binary is going to run on the target regardless of availability of specific libraries like glibc.
- `GOOS=linux`: Build a linux binary
- `GOARCH=arm`: The target architecture is ARM
- `GOARM=7`: Specifically: ARMv7
- `go build -o build/nray-armv7-linux ./nray.go`: Take `nray.go` and compile it to `build/nray-armv7-linux`
- `-ldflags "-s -w"`: Omits symbol tables and debug information. This mostly reduces the size of the binary but should be disabled first when tracking down bugs.

That's it. No fighting the cross compiler or installing dependencies for ARM. `build-localarch` introduces more cool features, especially for developing nray or running in constrained environments:

~~~make
build-localarch:
	go build -race -o build/nray ./nray.go 
	go build -race -ldflags "-X main.server=127.0.0.1 -X main.port=8601" -o build/nray_localhardcoded ./nray.go 
~~~

This target creates two binaries: `nray` and `nray_localhardcoded`. 
Both are targeting the architecture and operating system of the build machine.
CGO is not disabled in order to use the race detector of Go. The race detector is a really powerful feature that allows to detect concurrent, not synchronized access to data. Since nray heavily depends on Go's concurrency features, the race detector is probably the main reason why nray does not blow up every ten seconds, so if you're working on the code base it is highly advised to enable it.

In contrast to the `nray` binary, `nray_localhardcoded` has values for the server and port address injected at compile time. Running `nray_localhardcoded` without any parameters (e.g. by double clicking) will connect to `127.0.0.1:8601` which may come in handy in some situations <i class="far fa-grin-wink"></i>