# Lab: Executing AIP 2.0 Protocols

## Overview

In this lab, we’ll go back to you being the controller using the OpenAPI/Swagger interface, but this time using the AIP 2.0 protocols.

## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:

- [Running LFS173x Labs](RunningLabs.md)
  
## Instructions

The instructions for this lab can be found [here](https://aca-py.org/latest/demo/AliceWantsAJsonCredential/) on the ACA-Py Documentation site. The lab covers
the AIP 2.0 protocols for connecting, and uses the JSON-LD verifiable credential formats (BBS+ and LD Signatures). To exchange the JSON-LD format verifiable credentials version 2.0 if the
Issue Credential and Present Proof protocols are used. Note that while not demonstrated in the lab, Indy AnonCred format credentials can also be exchanged using the version 2.0 credential
exchange protocols.

## Takeaways

This lab demonstrates invoking HTTP ACA-Py Admin endpoints used by controllers (in this case, you) to execute Aries AIP 2.0 protocols. The
sequence was pretty much the same as the last lab you did, but with a different set of protocols. The lab showed:

- Controllers initiating several protocols:
  - Faber creating an invitation to share with Alice ([RFC 0434 Out-of-Band](https://github.com/hyperledger/aries-rfcs/tree/main/features/0434-outofband))
  - Alice requesting a connection based on the invitation ([RFC 0023 DID Exchange](https://github.com/hyperledger/aries-rfcs/tree/main/features/0023-did-exchange))
  - Faber initiating an issue credential V2 protocol ([RFC 0453](https://github.com/hyperledger/aries-rfcs/tree/main/features/0453-issue-credential-v2))
  - Faber issuing a JSON-LD BBS+ verifiable credential ([RFC 0646](https://github.com/hyperledger/aries-rfcs/tree/main/features/0646-bbs-credentials))
  - Faber initiating a present proof V2 protocol ([RFC 0454](https://github.com/hyperledger/aries-rfcs/tree/main/features/0454-present-proof-v2))
  - Faber using the DIF Presentation Exchange data format to request the presentation ([RFC 0510](https://github.com/hyperledger/aries-rfcs/tree/main/features/0510-dif-pres-exch-attach))
- Events from ACA-Py being received by controllers via a webhooks as the protocol moves forward.
- The controller pulling data from the events to process and respond to those events.

This lab provides another example of the inner workings of controllers as they step through Aries protocols. Although a lot has changed between AIP 1.0 and AIP 2.0, the Admin and API
and the interactions between controllers and agent frameworks remain (at least conceptually) the pretty much the same.

That's it for this lab! Please return to the course.
