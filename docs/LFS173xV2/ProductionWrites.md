# Lab: Scripting Production Writes

## Overview

In this lab, we'll show a series of scripts that can be used to write to an Indy
ledger (such as the Sovrin MainNet) when your agent is not an endorser and so is
not permitted to write directly to the ledger. What is required is that your
agent must prepare and sign the transaction, pass the transaction to an endorser
to sign, and then either the author or the endorser can submit the doubly-signed
transaction to the ledger.

## How to Run

This lab can only be run locally with Docker. For general instructions for on running locally with Docker, see the following:

- [Running LFS173x Labs](RunningLabs.md#running-on-docker-locally)

## Instructions

You are going to production on a fully permissioned Indy ledger (like the Sovrin
MainNet), you need to create some objects on the ledger (e.g. a schema and
credential definition), and you don’t have a DID that is permitted to write to
the ledger. In Indy terms, you are a transaction author, and you need a
transaction **endorser** to sign your transactions before they can be written to
the ledger.

As you will see, the process is pretty laborious&mdash;be glad you didn't have
to create all the scripts we'll be using! Don’t worry&mdash;the mechanics of
doing this have gotten easier since this was put together. However, we think
this is a good exercise to go through to understand the interactions that must
happen. Even when the process is fully automated within a framework, the steps still have to happen.

Further, as you do these operations, please note that you are updating your
agent’s secure storage database and so you must make sure the database is
preserved. Once the process is complete, the agent that will ultimately use
these objects (the DIDs, schema and credential definitions) **must** use the
same secure storage database. An example is given of how to backup a secure
storage database (using export) as part of the process.

To run the lab, see the [instructions
here](https://github.com/bcgov/von-network/blob/main/docs/Writing%20Transactions%20to%20a%20Ledger%20for%20an%20Un-privileged%20Author.md).
As noted above, these steps must be run with using Docker locally. It does
**NOT** work using Play with Docker.

## Takeaways

In completing this lab you will see the complexity that comes from having a
permissioned ledger, where (in some cases) transactions must be signed and
written to the ledger by endorsers on behalf of those without write permissions.

As you complete the exercise, consider how this process could be improved (it
couldn’t get any worse!). In Aries Cloud Agent Python, the solution has
been fully automated:

- An entity with an Endorser DID (a DID with permissions to endorse transactions
on an Indy ledger) runs an instance of the [Aries Endorser Service].
  - The [Aries Endorser Service] is a repository containing a configuration of
  ACA-Py suitable for use as an Endorser on a specific Indy Ledger.
- One or more ACA-Py instances with author DIDs (DIDs on an Indy ledger
  without permission to write a transaction to the ledger) are configured to
  use the [Aries Endorser Service] instance when needed.
- When an author needs to write a transaction to an Indy ledger, they prepare
the transaction and then send it to their designated [Aries Endorser Service].
- Upon receiving a transaction from an authorized Aries author, the [Aries
Endorser Service] endorses the transaction and returns it to the author.
- The author submits the endorsed transaction, which will be accepted and written to the ledger.

Note that there is special handling for creating the DID on the ledger for the
author. In that case, the author requests the DID be written by the Endorser,
and the Endorser creates, signs and submits the transaction to the ledger, and
returns the status (success or failure) of the process to the author.

[Aries Endorser Service]: https://github.com/hyperledger/aries-endorser-service

That's it for this lab! Please return to the course.
