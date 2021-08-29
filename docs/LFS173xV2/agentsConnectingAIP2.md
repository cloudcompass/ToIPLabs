# Lab: Agents Connecting<!-- omit in toc -->

- [Overview](#overview)
- [How to Run](#how-to-run)
- [Instructions](#instructions)
- [Takeaways](#takeaways)

## Overview

In this lab, we spin up a couple of Aries agents, establish connections between
them and have them exchange messages using the Aries `Basic Message` Protocol.
So, same as the [last lab](agentsConnecting.md), but this time we use the AIP
2.0 RFCs for establishing connections, [RFC 0434
Out-of-Band](https://github.com/hyperledger/aries-rfcs/tree/main/features/0434-outofband)
and [RFC 0023 DID
Exchange](https://github.com/hyperledger/aries-rfcs/tree/main/features/0023-did-exchange).

## How to Run

This lab from the ACA-Py repository includes details about running the example
locally using Docker, on Play with Docker, and even has some guidance on running
the lab without Docker. As always, we recommend running the lab using Docker, so
you don’t get bogged down in technical issues unrelated to the lessons of the
lab.

## Instructions

We're going to use the same instructions (below) as we used for the last lab,
but when starting the Faber agent, please use the following command, with the
extra option:

```bash
./run_demo faber --did-exchange --aip 20

```

What's the difference? Not very much... The only difference you will see is that
the in the invitation, the message will be of type `out-of-band/1.0/invitation`
instead of the AIP 1.0's `connections/1.0/invitation`. Not much to see, but
quite a bit different within the ACA-Py framework code -- full implementations of
the Out of Band and DID Exchange protocols, beside the Connections protocol. There
is a little bit of code in the controllers to handle both ways of establishing the
connection, but not much, and no change at all once the connection is in place.
Whether the connection is established using [RFC 0160
Connections](https://github.com/hyperledger/aries-rfcs/tree/main/features/0160-Connections)
or the AIP 2.0 connection RFCs ([RFC 0434
Out-of-Band](https://github.com/hyperledger/aries-rfcs/tree/main/features/0434-outofband)
and [RFC 0023 DID
Exchange](https://github.com/hyperledger/aries-rfcs/tree/main/features/0023-did-exchange)),
the same connection object results, and the rest of the code (ACA-Py and the
controller) is unaffected.

So, remembering the extra option and what to look at to see the difference,
complete the lab by following the [instructions
here](https://github.com/hyperledger/aries-cloudagent-python/tree/master/demo#the-alicefaber-python-demo),
stop once the connection is established. The astute participants will notice
that we don't add the extra option to the Alice agent. That's because Faber is
initiating the invitation, and has to be told what version of invitation to
generate, whereas Alice is receiving the invitation. Her agent can determine
from the message `@type` what protocol is being used, and respond accordingly. That
is an example of how protocols are deprecated in Aries:

- Step 1: Agents (frameworks and deployments of agents) are updated to accept both the old
and new protocols, while continuing to initiate protocols the old way.
- Step 2: Agents are updated to initiate the interactions with the new protocol.
- Step 3: Agents are updated to drop the old protocols, and use only the new ones.

Ideally, all Aries deployments complete Step 1 before all go to Step 2, and all complete
Step 2 before all go to Step 3. In doing that, interoperability is maintained throughout
the transition. This is described in
[RFC 0345 Community Coordinated Update](https://github.com/hyperledger/aries-rfcs/tree/main/concepts/0345-community-coordinated-update). For
the "Connections to DID Exchange" transition, the process is defined in [RFC 0496](https://github.com/hyperledger/aries-rfcs/tree/main/features/0496-transition-to-oob-and-did-exchange).

<!----- ## Navigating the Code

Now let’s take a look at the controller code. We’ll cover here the important parts of the controllers starting up, connecting and sending text messages. In a later lab, we’ll complete the demo through issuing and proving verifiable credentials and cover those parts of the controller code. Since we aren’t dealing with verifiable credentials in this part of the code walk through, little of what is covered here relates to Indy or an Indy ledger.

Note that the links to specific lines in the code go to a specific version (commit) of the file in GitHub that may not be the latest. As such, the line numbers in GitHub may be slightly different than what is on your system (the latest version).

- Alice agent code is in the repo file [demo/runners/alice.py](https://github.com/hyperledger/aries-cloudagent-python/blob/master/demo/runners/alice.py)
- Faber agent code is in the file [demo/runners/faber.py](https://github.com/hyperledger/aries-cloudagent-python/blob/master/demo/runners/faber.py)
- Both Alice and Faber are instances of [demo/runners/support/agent.py](https://github.com/hyperledger/aries-cloudagent-python/tree/master/demo/runners/support/agent.py)

### Faber Controller

#### Agent Startup

- The [“main” function](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L117) to start the controller and agent.
  - “genesis = await …” get the genesis file for the reading/writing to the ledger.
  - “agent = FaberAgent …” start an agent instance.
    - Call to the (parent) [controller class](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L31) to initialize the controller.
    - Note the specific details about Faber (e.g. port numbers) and the extra ACA-Py startup parameters just for Faber.
  - “await agent.listen_webhooks …” setup for receiving events from ACA-Py.
    - Parent [method](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/support/agent.py#L307) that initializes webhooks and route handlers.
      - Note below the functions for receiving and handling webhooks from ACA-Py. These functions are called when an event happens in ACA-Py that the controller needs to know about.
      - Also just below that are the admin calls (request, GET and POST) for the controller to invoke the ACA-Py endpoints.
  - “await agent.start_process … “ call to startup the ACA-Py instance process.
    - Parent [method](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/support/agent.py#L269) that starts the ACA-Py instance sub-process.
      - The ACA-Py process is separate from the controller process.
    - “agent_args = …” prepare ACA-Py startup arguments.
      - [Function](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/support/agent.py#L160) that gathers all the ACA-Py arguments to use, defaults, specific ports, URLs, wallet (storage info), optional demo arguments and controller-specific arguments. So many!!!
      - Recall our earlier look at all of the possible ACA-Py startup arguments as you look at how many we are using in this example.
- The [method in the agent class](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/support/agent.py#L75) to initialize the controller instance.
  - Like ACA-Py, many parameters may be passed in to control specific behavior. As seen above, Faber only specifies a handful of those parameters.
  - “self.ident = …“ defaulting of parameters as needed.
  - “if RUN_MODE …” is special handling to support running on “[Play with Docker](https://labs.play-with-docker.com/)”.
  - “self.storage_type = …” specify the type and details of the agent storage to be used.
    - The demo supports (with appropriate configuration) the use of SQLite (default) or PostgreSQL Indy agent storage.
    - Although still part of the indy-sdk, agent storage will soon be moved from Indy to Aries, as there is not an Indy (DID ledger, credential exchange) element to agent storage.

#### Connection Invitation Creation

- [Generate](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L159) an invitation that Alice can use to connect.
  - “connection = await …” call to ACA-Py to create an invitation.
  - “await agent.detect_connection …” wait a response to the invitation.

#### User input Processing

- [Main loop](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L175) for processing command line input from the user.

#### Send a Basic Message

- The user [chose Option 3](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L246), send a message.
  - Prompt for the message.
  - “await agent.admin_POST …” invoke ACA-Py to start an instance of the Basic Message protocol ([RFC 0095](https://github.com/hyperledger/aries-rfcs/tree/master/features/0095-basic-message)).

### Alice Controller

#### Agent Startup

The startup of the Alice controller is almost the same as Faber, so we’ll leave the review of that part of the code as an exercise for the reader. Much of the differences between the two in the areas that relate to the handling of verifiable credentials, which we cover in a later exercise.

#### Accept Invitation

- [Prompt for and receive the text invitation](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/alice.py#L167), as pasted in by the user.
  - “try … url = …“ first try at parsing the invitation text.
    - The controller allows flexibility in what the user pastes in. It could be a URL with a base64 invitation as a query parameter, only the base64 query parameter, or the already decoded JSON of the invitation.
    - Or it might be an improperly constructed invitation and so not a valid invitation at all.
  - “connection = await …” invokes the ACA-Py endpoint for processing a received invitation.
    - Since the “--auto-accept-invites” ACA-Py startup parameter is used, the controller just has to wait for the ACA-Py instance to complete the connection handling here: “await agent.detect_connection …”

#### User input Processing

- **[Main loop](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/alice.py#L232)** for processing command line input from the user.

#### Send a Basic Message

- The user [chose Option 3](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/alice.py#L237), send a message.
  - Prompt for the message.
  - “await agent.admin_POST …” invoke ACA-Py to start an instance of the Basic Message protocol ([RFC 0095](https://github.com/hyperledger/aries-rfcs/tree/master/features/0095-basic-message)).

While we won’t go into detail here about the internals of ACA-Py (since developers that write controllers don’t need to do that), for the curious, here are the links to the ACA-Py code for the [connections](https://github.com/hyperledger/aries-cloudagent-python/tree/master/aries_cloudagent/protocols/connections) and [basic message](https://github.com/hyperledger/aries-cloudagent-python/tree/master/aries_cloudagent/protocols/basicmessage) protocol handlers.

---->

## Takeaways

This lab demonstrates:

- Starting agents.
- Generating an (AIP 2.0) invitation using the pro appropriate protocols ([RFC 0434
  Out-of-Band](https://github.com/hyperledger/aries-rfcs/tree/main/features/0434-outofband)
  and [RFC 0023 DID
  Exchange](https://github.com/hyperledger/aries-rfcs/tree/main/features/0023-did-exchange)).
- Processing an invitation.

This lab also demonstrates how both Aries in general, and ACA-Py in particular
deals with the evolution of protocols. Both AIP 1.0 and AIP 2.0 connection
protocols are in active use in the community, and so both (for now) need to be
supported. Although the RFCs/protocols are different, the result of executing
the protocols are the same -- a connection is established. ACA-Py retained the
same concept of a connection object so that nothing else in existing controllers
needed to change. Eventually, the older AIP 1.0 "Connections" protocol will no
longer be used, and its code can be removed from Aries frameworks like ACA-Py.

Interested in the Alice/Faber controller code impacted by the change? Go to the
current main branch code in ACA-Py and scan the demo Python controllers for
references to `use_did_exchange` and `out-of-band`.

That's it for this lab! Please return to the course.
