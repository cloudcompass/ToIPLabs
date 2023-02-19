# Lab: Executing AIP 2.0 Protocols

## Overview

In this lab, we’ll go back to you being the controller using the OpenAPI/Swagger interface, but instead of using AnonCreds credentials, we'll use the JSON-LD credentials using the W3C Verifiable Credentials Data Model Standard.

## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:

- [Running LFS173x Labs](RunningLabs.md)
  
## Instructions

The instructions for this lab can be found [here](https://github.com/hyperledger/aries-cloudagent-python/blob/main/demo/AliceWantsAJsonCredential.md) in the ACA-Py repository. The lab  calls for the use of JSON-LD verifiable credential formats using BBS+ Signatures for JSON-LD. The protocol steps are the same, as you are still issuing and presenting
credentials. What changes are the data structures of the attachments--the data around the attributes and values within the credential.

As well as the credential data format differing from AnonCreds, the presentation request and presentation formats differ as well. The DIF ([Decentralized Identity Foundation](https://identity.foundation)) [Presentation Exchange](https://identity.foundation/presentation-exchange/) (DIF PE) format is used. DIF PE is a general purpose protocol that can be used with many types of verifiable credentials. There has been some discussion of using the DIF PE with AnonCreds and it seems like it could be a good fit. To this point, the AnonCreds presentation request format has been sufficient, but it would not be surprising to see DIF PE used with AnonCreds verifiable credentials in the future.

## Takeaways

This lab demonstrates invoking HTTP ACA-Py Admin endpoints used by controllers (in this case, you) to exchange credentials in JSON-LD format using the W3C Verifiable Credentials Data Model Standard. The lab demonstrates:

- Controllers initiating several protocols:
  - Faber creating an invitation to share with Alice ([RFC 0434 Out-of-Band](https://github.com/hyperledger/aries-rfcs/tree/main/features/0434-outofband))
  - Alice requesting a connection based on the invitation ([RFC 0023 DID Exchange](https://github.com/hyperledger/aries-rfcs/tree/main/features/0023-did-exchange))
  - Faber initiating an issue credential V2 protocol ([RFC 0453](https://github.com/hyperledger/aries-rfcs/tree/main/features/0453-issue-credential-v2))
  - Faber issuing a JSON-LD BBS+ verifiable credential ([RFC 0646](https://github.com/hyperledger/aries-rfcs/tree/main/features/0646-bbs-credentials))
  - Faber initiating a present proof V2 protocol ([RFC 0454](https://github.com/hyperledger/aries-rfcs/tree/main/features/0454-present-proof-v2))
  - Faber using the DIF Presentation Exchange data format to request the presentation ([RFC 0510](https://github.com/hyperledger/aries-rfcs/tree/main/features/0510-dif-pres-exch-attach))
- Events from ACA-Py being received by controllers via a webhooks as the protocol moves forward.
- The controller pulling data from the events to process and respond to those events.

One element of the presentation process that is left as an exercise for the implementation is what the verifier knows about the relationship between the holder and the credential. As we have covered in the course, the use of the AnonCreds "blinded link secret" is used to show that the holder sharing a presentation to a verifier is the same holder to which the issuer issued the credential. The holder proves (using a zero-knowledge proof) that they know the link secret that was put into the signed credential by the issuer. With the JSON-LD-based signatures used with W3C Verifiable Credentials Data Model Standard, there is no corresponding feature to link the holder to the credential. Such a binding is not defined and it is left to implementations to determine if it is important for a given use case, and if it is, how to achieve it. The technique used in this lab is to have the holder put a `did:key` DID into the credential, and then during presentation, prove control over the DID--prove that they know the private key related to the DID. Conceptually, that approach is similar to the use of the link secret in AnonCreds (same interactions), with the exception that the DID is a unique, correlatable identifier for the holder.

That's it for this lab! Please return to the course.
