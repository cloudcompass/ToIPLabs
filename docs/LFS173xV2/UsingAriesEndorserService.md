# Lab: Using the Aries Endorser Service

## Overview

We'll use the familiar Alice-Faber demo, adding to the fun an instance of the Endorser service
that Faber will use when writing to the ledger.

## How to Run

This lab can only be run locally with Docker. For general instructions for each, see the following:

- [Running LFS173x Labs](RunningLabs.md#running-on-docker-locally)

## Instructions

Start a terminal session in an appropriate folder, and execute the following commands to get
a local copy of Aries Cloud Agent Python (ACA-Py), if you don't have one already.

```bash
git clone https://github.com/hyperledger/aries-cloudagent-python
cd aries-cloudagent-python/demo

```

The instructions for the demo can be found on the ACA-Py [Endorser Demo](https://github.com/hyperledger/aries-cloudagent-python/blob/main/demo/Endorser.md) page. The instructions are a bit sparse compared
to the main [Alice-Faber demo instructions](https://github.com/hyperledger/aries-cloudagent-python/tree/main/demo#the-alicefaber-python-demo), but hopefully they are enough to get you through it.

The main differences from a regular Alice-Faber demo run are:

- The demo uses revocation, so in addition to starting a local VON Network
  Hyperledger Indy instance, you need to start up a local Tails Server.
- A parameter on the startup of Faber `--endorser-role author` to indicate that Faber
requires an Endorser.
- As Faber writes objects to the ledger, including those related to revocation,
  their transactions are passed to an Endorser and signed.

Watch the terminal output as you go through the demo to see the Endorser flow happening every time Faber must write
to the ledger. Per the setup of the example, with every 5 credentials issued to Alice, a new revocation registry will
be started, requiring extra ledger writes, and hence, additional endorsements.

There is a second demo that shows what happens in setting up a DID as an author. In that demo, Faber is the Endorser and
Alice is the author. Give it a try as well.

### Navigating the Code

As we did with the Faber and Alice code, let’s take a quick look at the code for this demo, focusing on the impact of the Endorser role in the configuration. There is not a lot to it!

If Faber starts as an Author (`--endorser_role author` -- checked
[here](https://github.com/hyperledger/aries-cloudagent-python/blob/467104fab662507e18483abaaf2305bc702bb303/demo/runners/faber.py#L419))
the demo `create agent` process creates an extra agent, the Endorser
[here](https://github.com/hyperledger/aries-cloudagent-python/blob/467104fab662507e18483abaaf2305bc702bb303/demo/runners/support/agent.py#L1362).
The extra agent is an ACA-Py agent that is configured to be an Endorser, with a
specific Endorser DID known. This "no configuration" set up of an Endorser DID
is possible because it is using a sandbox instance of Indy, which has a
well-known Endorser DID. In a production or public ledger use of an Endorser,
the Endorser DID would have to have been setup ahead of time, sometimes with
legal documents to be signed and a fee to be paid.

Faber is started with configuration settings that set the
extra agent as the Endorser to be used when needed. That configuration is all the Faber controller needs to do, ACA-Py takes care of the rest. When executing operations that require
writing to the ledger, the ACA-Py code will detect that it's running as an author and execute the extra steps needed to
get the Endorser signature without bothering the Controller. No extra code needed in the controller to use an endorser!

The underlying message? Adding in the use of an Endorser has a small impact on the configuration of the controller/ACA-Py combination, but has no impact on anything else.

> **Note:** The links in these instructions to specific lines in the code go to a
specific version (commit) of the files in GitHub that may not be the latest. As
such, the line numbers in GitHub may be slightly different than what is on your
editor (the latest version on the main branch). The links are using commit
467104fab662507e18483abaaf2305bc702bb303 from February 11, 2023.

## Takeaways

The key takeaway from this lab is how the Hyperledger Indy endorser process can be integrated into agent-to-agent scenarios with minimal impact to the agent controller code. Notifying the agents (authors and the Endorser) of their
roles using startup parameters is all that is needed. The Endorser does need to have its DID setup ahead of time, with
whatever process is needed by the ledger on which it is operating.

That's it for this lab! Please return to the course.
