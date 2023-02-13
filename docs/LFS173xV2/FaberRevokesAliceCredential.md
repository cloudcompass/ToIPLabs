# Faber Revokes Alice's Credential

## Overview

In this lab, we'll take the earlier Alice and Faber College lab a little further, demonstrating using the demo
with Alice as a Mobile Agent, and having Faber revoke Alice's credential. It's amazing how a little bit of code
in the Alice-Faber demo can be tweaked to support so many variations!

## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:

- [Running LFS173x Labs](RunningLabs.md)

## Instructions

We’re again going to use the tutorial in the ACA-Py repository to spin up agents for Alice and Faber, have them connect, exchange messages and issue and prove a verifiable credential. Follow the [instructions here](https://github.com/hyperledger/aries-cloudagent-python/blob/main/demo/AliceGetsAPhone.md). The differences from the previous runs of
the Alice-Faber demo we have run are:

- We have to run a Revocation Tails Server to run the demo.
- Since we are using mobile agents, we have to use a public Indy Ledger. In this case, we are using BCovrin Test.
- We're only running Faber on in Play-With-Docker or locally with Docker. Alice
  is using a mobile wallet on your smartphone.
- We start the Faber instance with some extra options, including a flag activating revocation for the demo instance.

Other than that, you should find the instructions pretty similar. Give it a try!

By the way, this lab can be done without the mobile phone part. You still need to have the extra tails server, but you can run the Alice command line agent exactly as you did in the initial Alice-Faber scenario. When Faber has revocation activated, the extra commands are available, and you can use the just as with the mobile demo. The details of that are outlined [here](https://github.com/hyperledger/aries-cloudagent-python/blob/main/demo/README.md#revocation) in the demo folder's README.md file. Don't forget to start the Tails Server before you begin!

## Takeaways

In this lab we’ve seen a command line example of an agent issuing, revoking and verifying credentials, and used an Aries Mobile wallet for the holding and proving credentials. In doing the revocation, we've seen how wallets can handle the 
situation where a credential being asked for by a verifier is revoked.  Should the wallet allow a presentation to be sent
includes a credential that is revoked?

From a controller perspective, the updates needed to revoke a credential are pretty minor--what you would expect to meet the business needs of revoking credentials. Underneath though, within ACA-Py, there is a lot more going on, with extra writes the ledger needed from time to time. Happily, all that complexity is hidden from the controller.

That's it for this lab! Please return to the course.
