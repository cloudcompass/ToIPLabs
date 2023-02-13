# Lab: Executing Aries Protocols Using OpenAPI/Swagger

## Overview

In this lab, we’ll go back to you being the controller. We'll use an OpenAPI/Swagger user interface to allow you to be an Aries agent controller. As well, we’ll use a couple of demo options to ensure you are executing each step of the protocols, and that you are seeing the webhook data that comes back from ACA-Py. In this way, you will be seeing and preparing the data exactly as would a controller.

## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:

- [Running LFS173x Labs](RunningLabs.md)

## Instructions

The instructions for this lab can be found [here](https://github.com/hyperledger/aries-cloudagent-python/blob/main/demo/AriesOpenAPIDemo.md) in the ACA-Py repository. As you carry out the instructions, keep track of who you are on each step (Alice’s or Faber’s controller) and consider how you would code an application to automate the manual steps in a generalized way.For example:

- If you really were Faber’s controller, how would you handle executing thousands of protocol instances running in parallel between you and all of Faber’s alumni?
- How would you interface with Faber College’s backend information systems?
- How would you structure Alice’s controller if her Aries agent was running on her phone?

## Takeaways

This lab demonstrates executing the HTTP interfaces used by instances of ACA-Py and their controllers (in this case, you) to execute Aries protocols. It shows:

- Controllers initiating several protocols:
  - Faber generating an invitation using the AIP 1.0 Connections protocol ([RFC 0160](https://github.com/hyperledger/aries-rfcs/blob/main/features/0160-connections/README.md)).
  - Alice responding to the invitation using AIP 1.0 Connections protocol ([RFC 0160](https://github.com/hyperledger/aries-rfcs/blob/main/features/0160-connections/README.md)).
    - The use of the AIP 1.0 protocols in the demo instructions (as of February
    2023) need to be updated to use the AIP 2.0 [RFC 0434
    Out-of-Band](https://github.com/hyperledger/aries-rfcs/blob/main/features/0434-outofband/README.md)
    and [RFC 0023
    DID-Exchange](https://github.com/hyperledger/aries-rfcs/blob/main/features/0023-did-exchange/README.md)
    protocols for generating the invitation and responding to the invitation,
    respectively. If that update to the demo has not yet been done, you might
    want to see if you can use those protocols to establish the connection
    between the two agents. Either way, the resulting connection is the same.
  - Alice initiating a basic message protocol ([RFC 0095](https://github.com/hyperledger/aries-rfcs/tree/main/features/0095-basic-message)).
  - Faber initiating an issue credential protocol ([RFC 0453](https://github.com/hyperledger/aries-rfcs/tree/main/features/0453-issue-credential-v2/README.md)).
  - Faber initiating a present proof protocol ([RFC 0454](https://github.com/hyperledger/aries-rfcs/tree/main/features/0454-present-proof-v2/README.md)).
- Events from ACA-Py being received by controllers via a webhooks as the protocol moves forward.
- The controller pulling data from the events to process and respond to those events.

This lab provides a good introduction to the inner workings of controllers as they step through Aries protocols. It also makes it easy to see the interactions between the controller, the agent framework (ACA-Py in this case) and other agents.

That's it for this lab! Please return to the course.
