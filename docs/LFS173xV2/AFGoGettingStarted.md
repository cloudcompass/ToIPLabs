# Lab: Getting Started with Aries Framework Go

## Overview

In this lab, we'll do many of the same things that we've done with Aries Cloud
Agent Python using Aries Framework Go, showing the similarities, and the
differences between the two Aries implementations. Remember the Swagger/OpenAPI
demo we did with ACA-Py? Time to do it again, but this time with Aries Framework
Go. The page is going to look the same, the techniques are the same, and the API
will be quite similar (although not exact). And remember, with Aries Framework
Go, you won't see much of Hyperledger Indy. While Hyperledger Indy DIDs can be
resolved with Aries Framework Go, you can't write those DIDs, nor can you read
or write any of the other Hyperledger Indy objects (schemas, cred-defs, etc.).
That means no issuing, holding or verifying Indy AnonCreds verifiable
credentials.

## How to Run

This lab can be only be run locally with Docker, although there are a couple of additional dependencies to be installed. For general instructions for running locally, see the following:

- [Running LFS173x Labs](RunningLabs.md)

The additional [Aries Framework Go prerequisites](https://github.com/hyperledger/aries-framework-go/blob/main/docs/test/build.md#Prerequisites-(for-running-tests-and-demos)) are `Go` (of course!), `make` and `node.js`.  It's quite possible you have them on your system already, but if not, here are the installation instructions:

- [Go installation instructions](https://golang.org/doc/install).
- Before trying to install `make`, check to see if you have it already by running `make` from your bash command line. Chances are you do, especially on Linux and Mac. If you are on Windows and don't have it, and you use [Chocolatey](https://community.chocolatey.org/), you can use that to install make (`choco install make`). If not, here are some [instructions to get it if you are using git bash](https://gist.github.com/evanwill/0207876c3243bbb6863e65ec5dc3f058).
- Instructions to [install node.js can be found here](https://nodejs.org/en/download/).

## Instructions

Once you have the prerequisites installed, clone the Aries Framework Go repository to your local system:

```bash
git clone https://github.com/hyperledger/aries-framework-go
cd aries-framework-go

```

Once there, open [these instructions](https://github.com/hyperledger/aries-framework-go/blob/main/docs/rest/openapi_demo.md) in the Aries Framework Go repo to run the OpenAPI Demo. We recommend doing at least the Alice/Bob section, to get a feel for the API, but there are other interesting things to try:

- The demo spins up some routing agents (Carl and Dave), and you can run through connecting Bob and Alice through a routing agent each. This is a great demo of the concepts covered in Chapter 6 on Routing.
- The custom message handling segment covers extending the AIP 2.0 protocols to include a protocol not covered by the Aries protocols (`https://didcomm.org/generic/1.0/message`).
- The Aries Framework Go team designed the Aries RFC [HTTP over DIDComm RFC 0335](https://github.com/hyperledger/aries-rfcs/tree/main/features/0335-http-over-didcomm), and one of the demos demonstrates an implementation of the protocol.
- Finally, there are some AIP 2.0 demonstrations of using the Out-of-Band invitation to establish a connection, and credential exchange (issue credential, present proof).

You can spend lots of time with Aries Framework Go, as it, along with companion projects [DID Method `did:orb`](https://github.com/trustbloc/orb) and the [TrustBloc Wallet](https://github.com/trustbloc/wallet) make up a complete technical ecosystem.

## Takeaways

In completing this lab, you will see for yourself how the Aries protocols are truly the core of Aries. While there are different implementations of Aries guided by different goals, interoperability is possible because of that core. The OpenAPI demo shows that two Aries connecting look pretty much the same from a controller's perspective, regardless of the frameworks involved.

Want to check on the interoperability between Aries Framework Go and Aries Cloud Agent Python? Remember to check out [https://aries-interop.info](https://aries-interop.info) to see the latest!

That's it for this lab! Please return to the course.
