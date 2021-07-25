# Lab: Alice Gets a Credential<!-- omit in toc -->

- [Overview](#overview)
- [How to Run](#how-to-run)
- [Instructions](#instructions)
  - [Faber Controller](#faber-controller)
    - [Issuer Initialization](#issuer-initialization)
    - [Request From User to Issue Credential](#request-from-user-to-issue-credential)
    - [Request From User to Send Proof Request](#request-from-user-to-send-proof-request)
  - [Alice Controller](#alice-controller)
    - [Credential Offer Received](#credential-offer-received)
    - [Proof Request Received](#proof-request-received)
- [Takeaways](#takeaways)

## Overview

In this lab, we'll take the earlier Alice and Faber College lab a little further, demonstrating the issuance of a verifiable credential from Faber to Alice, and then Faber requesting proof based on the credential from Alice. While there is not much new to see in running this example, we’ll be drilling into the places in the controller code where all the key events are handled.

## How to Run

This lab from the ACA-Py repository includes details about running the example locally using Docker, on Play with Docker, and even has some guidance on running the lab without Docker. As always, we recommend running the lab using Docker, so you don’t get bogged down in technical issues unrelated to the lessons of the lab.

## Instructions

We’re again going to use the tutorial in the ACA-Py repository to spin up agents for Alice and Faber, have them connect, exchange messages and issue and prove a verifiable credential. Follow the [instructions here](https://github.com/hyperledger/aries-cloudagent-python/tree/master/demo#the-alicefaber-python-demo), this time completing the full tutorial.

When we ran this code in an earlier lab, we linked to the specific lines of controller code that handled the early part of the demo. Here are the key elements of the credential exchange handling within the controllers. Recall that the actual calls to the `indy-sdk` are embedded in ACA-Py, and the controller just has to use the REST API exposed by the API agent to trigger and handle the agent-related actions.

**Note:** _The links to specific lines in the code go to a specific version of the file in GitHub that may not be the latest. As such, the line numbers in GitHub may be slightly different than what is on your system (the latest version)._

- Alice agent code is in the repo file [demo/runners/alice.py](https://github.com/hyperledger/aries-cloudagent-python/blob/master/demo/runners/alice.py)
- Faber agent code is in the file [demo/runners/faber.py](https://github.com/hyperledger/aries-cloudagent-python/blob/master/demo/runners/faber.py)
- Both Alice and Faber are instances of [demo/runners/support/agent.py](https://github.com/hyperledger/aries-cloudagent-python/tree/master/demo/runners/support/agent.py)

### Faber Controller

#### Issuer Initialization

- Faber [registers a DID on the ledger](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L132), as required of a verifiable credential issuer.
  - [Method in agent.py](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/support/agent.py#L204) to call ACA-Py to register the DID.
    - Note in the method the use of environment variables (e.g. “LEDGER_URL”) and the default that we are using is a local VON Network (the reference to port 9000).
    - The controller assumes the ledger has a “/register” endpoint for registering a DID, which is a specific feature of the VON Network.
    - We cover in the edX LFS173x, Becoming an Aries Developer course, initialization for production ledgers where those assumptions are removed.
  - [Generate a random seed](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/support/agent.py#L122) for the agent.
    - Allows us to run the demo many times on the same ledger with the same schema and credential definition versions.
- Faber [registers a schema and credential definition](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L140) on the ledger.
  - Sets the schema version using random numbers.
  - Sets the schema attributes with name, date, etc.
  - [Method in agent.py](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/support/agent.py#L136) to call ACA-Py to register the schema and cred def.
    - “... await self.admin_POST …” is the REST call to ACA-Py.

#### Request From User to Issue Credential

- Faber [handles the request](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L182) from the user to issue a credential.
  - Prepare the claims for the credential.
    - In a real system, this data would be a lookup into Faber’s Student Information System based on an input about who was asking for a credential.
  - “cred_preview = …” construct the values to be sent.
  - “offer_request = …” prepare to send the request to Alice.
    - Note that the “connection_id” setting is hard coded - Faber only talks to Alice. That’s not very realistic!
    - In a real system, this is likely passed in as part of the “issue a credential” external event such as a web request.
  - “await agent.admin_POST…” send the credential offer to start the issue credential Aries protocol.
- Faber method to [issue the credential](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L60):
  - “cred_preview = …”  collect the passed in credential attributes
  - “await self.admin.POST…” initiate the “issue credential” Aries protocol ([RFC 0036](https://github.com/hyperledger/aries-rfcs/tree/master/features/0036-issue-credential))

#### Request From User to Send Proof Request

- Faber [handles the request](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L210) from the user to request a proof from Alice.
- Proof Request creation:
  - “req_attrs = …” specify restrictions that the claims must come from credentials issued by Faber’s DID.
    - Post Indy version 1.14, those claims can be group to a single restriction that would also require that the claims come from the same credential, versus (in this case) any credential issued by Faber’s DID.
  - “req_preds = …” require that the age be greater or equal to 18 and that the claim come from a credential issued by Faber’s DID.
  - “indy_proof_request = ... “ prepare the proof request data structure.
  - “proof_request_web_request = …” prepare the web request data structure.
  - “await agent.admin_POST ...” invoke ACA-Py to start the “present proof” Aries protocol ([RFC 0037](https://github.com/hyperledger/aries-rfcs/tree/master/features/0037-present-proof))

### Alice Controller

#### Credential Offer Received

- Alice’s [handler](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/alice.py#L59) for a webhook notification related to the issue credential protocol.
  - “state = …” get information about the instance of the protocol, including the state, the ID of the instance.
  - “if state == "offer_received"...” immediately send back a credential request response by invoking ACA-Py.
    - A real agent might popup a UI for Alice to see if she is interested in the credential offer that was received. Or maybe not. Since you are writing the controller, it can do whatever it needs to do to meet the business requirements.
  - “elif state == "credential_acked"...” handle the credential received event.
    - ACA-Py has already stored the credential in Alice’s wallet.
  - “resp = await …” invoke the ACA-Py REST endpoint to get the data from the credential back using the credential_id provided in the webhook and print the data to the log.

#### Proof Request Received

- Alice’s [handler](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/alice.py#L94) for a webhook notification related to the present proof protocol.
  - “state = …” get information about the instance of the protocol, including the state, the ID of the instance.
  - “if state == "request_received"...” start of processing to prepare the proof.
    - A real agent might popup a UI for Alice to see if she is interested in responding to the proof request.
  - “credentials = await ...” invoke the ACA-Py endpoint to retrieve the credentials that can satisfy the proof request and map the credential claims to the “referents” (a term used in Indy code for claims in a proof request/proof) in the proof.
  - “for referent in … requested_attributes …” collect the claims of the proof from the found held credentials, including handling (using a hard-coded value) any requested self-attested claims; claims not from a credential held by the holder/prover.
    - In a real agent, lots of things could happen here.
      - Multiple credentials could have been found in Alice’s storage for the claims. In that case, some kind of logic would have been applied for selecting which claim to use. For example, defaulting the choice and asking Alice to confirm/change the selection.
      - A choice could have been made in logic (or by Alice) to hide some claims—to not reveal the values and prove only possession of the claims.
  - “for referent in … requested_predicates …” collect the predicates (the true/false calculated claims) for the proof.
  - “request = …“ combine the data into the “proof” data structure.
  - “await self.admin_POST …” invoke ACA-Py via the REST API endpoint to send the proof to the requesting agent (Faber, in this case).
    - The presentation_exchange_id links the response to the protocol instance request.

While we won’t go into detail here about the internals of ACA-Py (since developers that write controllers don’t need to do that), for the curious, here are the links to the ACA-Py code for the [issue credential](https://github.com/hyperledger/aries-cloudagent-python/tree/master/aries_cloudagent/protocols/issue_credential) and [present proof](https://github.com/hyperledger/aries-cloudagent-python/tree/master/aries_cloudagent/protocols/present_proof) protocol handlers. Look into the “v1.0” folder for the Python code. And of course, those really interested can drill down into the Indy SDK, and even deeper into Ursa.

## Takeaways

In this lab we’ve seen a simple command line example of agents issuing, holding, proving and verifying credentials. We’ve also walked through the places in the controller code where the key events in the processes happen. The creation of controllers are at the core of what an Aries developer does, so this lab is crucial in understanding that task.

That's it for this lab! Please return to the course.
