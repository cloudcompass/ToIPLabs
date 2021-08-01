# Lab: Resolving DIDs Universally

## Overview

While Hyperledger Aries started using only Hyperledger Indy ledgers and Indy DIDs, it has expanded to handle
many types of DIDs. In fact, configured appropriately, Indy can deal with any DID method, by using an
instance of a Universal Resolver. In this lab we're going to play with a Universal DID Resolver.

## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:

- [Running LFS173x Labs](RunningLabs.md)

## Instructions

We're going to start this lab in a browser by going to the [DIF Resolver](https://resolver.identity.foundation) website.
The website is a deployed instance of the [DIF Universal Resolver](https://github.com/decentralized-identity/universal-resolver/)
open source project, which aims to enable the resolution of all publicly accessible DIDs.
Entities that specify, implement and [register at W3C](https://w3c.github.io/did-spec-registries/#did-methods)
a DID Method can contribute a resolver for their DID Method to the Universal Resolver project.
Given a DID of any supported DID Method, an instance of the Universal Resolver returns the DIDDoc and DID Metadata (if any) associated with the DID.

Before we start resolving DIDs, click on the orange warning icon on the top left of the page and read the caveats. As of writing
this (mid-2021) there are two. The first ("DIDs are evolving...") is becoming less and less of a concern as time
goes by and the DID specification is hardened. The specification is a W3C "Proposed Recommendation", and will transition
from their to (hopefully) a standard in the near future. The second warning is more interesting, suggesting that as a
central resource, it should not be used for production. Rather, if you want to use a universal resolver capability,
you should deploy and operate your own, making sure that it is secure and serves your purpose. That's a good advice
and something to think about as you decide to expand the DIDs that you are willing to accept.

Given that, let's start resolving some DIDs. For each DID, copy the DID given, paste it into the "DID URL" text
box, click the `Resolve` button and look at the results. Generally, we care most about the "DID Document" tab,
as that is what an Aries Agent will want to use. However, you should also scan the other documents.

First, we can look at DID that I use as a part of the Sovrin Foundation, `did:sov:7Tqg6BwSSWapxgUDm9KKgg`. It's a DID
found on the Sovrin MainNet, as you can see from by looking at using [IndyScan.io](https://indyscan.io) by clicking [here](https://indyscan.io/tx/SOVRIN_MAINNET/domain/54474). Note the minimal information on the Sovrin Ledger--just a
DID and verkey, and the relatively long DID Document shown by the Universal Resolver. That's because the
[Sovrin DID Method](https://sovrin-foundation.github.io/sovrin/spec/did-method-spec-template.html)
defines how to transform a Sovrin MainNet DID into a DIDDoc, and it includes a number of standard entries
derived from just the minimal information stored on the ledger.

Next, let's look at a `did:web` DID method, and in particular, `did:web:did.actor:alice`. The `did:web` method is interesting.
It works by an entity with a DNS entry including it in the DID after `did:web` (so `did.actor` in our example) and then
having the full DIDDoc for the DID at the location `https://<dns>/<did>/did.json`. So, for Alice's DID above, we can get the
same DIDDoc by going to the web URL: [https://did.actor/alice/did.json](https://did.actor/alice/did.json). Try it!
The `did.actor` site has been set up as a demonstration, but it works for any DNS entry. If you have access to your own
web server, you can add a `did.json` document and resolve it as a DID. Cool stuff!

Another self-published DID Method (no distributed ledger needed!) is `did:github`, such as `did:github:gjgd`. Check
out the `did:github` DID Method and see if you can publish your own resolvable DID. The hardest part is generating
your private/public key pair for it. But if you can do that, you can easily publish a DID that is associated with your
github account.

Use the list of examples below the `did-url` text entry box to try resolving some other DIDs based on some other DID Methods.
As you can, find the corresponding DID Method specification linked from the
[W3C DID Method Registry](https://w3c.github.io/did-spec-registries/#did-methods) to learn about the DID method and to where
the DIDs are published. We suggest you look at examples for these DID Methods:

- `did:btcr` a DID on the Bitcoin ledger
- `did:erc725` a DID on the Ethereum ledger
- `did:ethr` another DID method using the Ethereum ledger
- `did:ion` a DID rooted in the Bitcoin ledger using Microsoft's DID Method
- `did:ipid` a DID based on the IPFS "Interplanetary File System"
- `did:key` a DID not on a ledger, just a public key wrapped in the DID itself

Enough resolving.

## Takeaways

We've shown how DID resolution works, including a couple of ways to have a published DID without having a distributed ledger,
and some DIDs published on some very big ledgers, such as Bitcoin and Ethereum.

As well, we've demonstrated the DIF Resolver, an instance of the "Universal Resolver" project, which is a (relatively) easy
way to deploy your own resolver with your Aries agents to resolve DIDs of as many (or as few) as you want.

That's it for this lab! Please return to the course.
