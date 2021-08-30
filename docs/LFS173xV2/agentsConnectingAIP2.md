# Lab: Agents Connecting<!-- omit in toc -->

- [Overview](#overview)
- [How to Run](#how-to-run)
- [Instructions](#instructions)
- [Navigating the Code](#navigating-the-code)
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

## Navigating the Code

Navigating the code is pretty straight forward in this case, there's not much different from the previous "Connecting..." lab we did. Recall from that where the code for the agents reside:

- Alice agent code is in the repo file [demo/runners/alice.py](https://github.com/hyperledger/aries-cloudagent-python/blob/master/demo/runners/alice.py)
- Faber agent code is in the file [demo/runners/faber.py](https://github.com/hyperledger/aries-cloudagent-python/blob/master/demo/runners/faber.py)
- Both Alice and Faber are instances of agents in the file [demo/runners/agent_container.py](https://github.com/hyperledger/aries-cloudagent-python/blob/master/demo/runners/agent_container.py)
- The Alice and Faber agents are instances of the DemoAgent class imported into agent container from [demo/runners/support/agent.py](https://github.com/hyperledger/aries-cloudagent-python/tree/master/demo/runners/support/agent.py)

During the connection process, the only differences in the demo controller code are:

- In the base agent, when creating an invitation, Faber has the "use_did_exchange" flag set to true to execute [this code for AIP 2.0 Out of Band and DID Exchange](https://github.com/hyperledger/aries-cloudagent-python/blob/d78d4ea483e76c8033141e3c6c8e1a68e3a72096/demo/runners/support/agent.py#L963).
- In the base agent, when Alice gets the invitation, the [message type of the invitation (AIP 1.0 or AIP 2.0) is detected](https://github.com/hyperledger/aries-cloudagent-python/blob/d78d4ea483e76c8033141e3c6c8e1a68e3a72096/demo/runners/support/agent.py#L982) and processed accordingly.

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
