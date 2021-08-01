# Lab: Dealing with a Ledger TAA

## Overview

Some Indy ledgers, especially production ledgers like Sovrin MainNet, use a mechanism called the Transaction Author Agreement (TAA) to ensure
that those writing to the ledger agree to the legal "terms of use" of the ledger. For the most part, the TAAs are usually intended to make sure
the author agrees not to write private data or anything illegal to post on the ledger. But the TAA can hold anything, so it's a good idea to
look at the document, or better, have your lawyer look at the details.

In this lab, we're just going to use the ACA-Py Admin API to retrieve and accept the TAA. We're not going to write any data to the ledger
since we won't have a DID that permits us to do that. But with a permissioned DID on the ledger, we could write data!

## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:

- [Running LFS173x Labs](RunningLabs.md)

## Instructions

To begin the lab, you need to clone the ACA-Py repo, if you haven't already got it locally. To do that, run these commands in your bash shell:

```bash
git clone https://github.com/hyperledger/aries-cloudagent-python
cd aries-cloudagent-python

```

If you have the repo cloned already, change to the root of the repository in a bash shell terminal session.

From the root of the clone repository, change into the demo folder and then we're going to start the Alice demo agent. However, instead of using
a sandbox ledger as we normally do, we're going to connect to Sovrin MainNet. There is definitely a TAA on that ledger!

```bash
cd demo
GENESIS_URL=https://raw.githubusercontent.com/sovrin-foundation/sovrin/master/sovrin/pool_transactions_live_genesis ./run_demo alice

```

Once Alice starts up and is waiting for her invitation to connect to Faber, open a browser tab on Alice's Admin API at [http://localhost:8031](http://localhost:8031).

We'll start by getting the TAA that is stored on the ledger. Execute the `GET /ledger/taa` endpoint to retrieve the TAA from the ledger.

In the result scan for the `text` JSON item to see the very (very!) long MainNet TAA. If you want a formatted version of the doc, you can review it
[here](https://sovrin.org/wp-content/uploads/Transaction-Author-Agreement-V2.pdf) on the Sovrin Foundation site. You will also see the "Acceptance
Mechanism List" (AML) in the `aml` item in the results JSON, within the `aml_record` item.

So what do we do that with? We need to use the `POST /ledger/taa/accept` endpoint to inform ACA-Py that we accept the TAA. ACA-Py will store that 
indication of acceptance and apply it on every write transaction to the Indy ledger. You need to do a bit of copying and pasting to accept the TAA:

- Click the "Try it Out" for the `POST /ledger/taa/accept`.
- From the results from the `GET /ledger/taa`, highlight, copy and paste the following values into the `POST /ledger/taa/accept` body.
  - The `version` value from the results and into the `version` field of the body (the easy one...).
  - Pick one of the `aml` types (e.g. `for_session`, `at_submission`, etc.) to put into the `mechanism` field of the body.
    - Usually the `at_submission` value is the right choice as ACA-Py will apply the TAA with each write.
  - The entire (!!!) `text` value from the results and into the `text` field of the body.
    - That's a lot of text! Copy it carefully...
- Execute the transaction and check the results.

If all goes well, you should have a `200` response status and an empty JSON result (`{}`). Execute the `GET /ledger/taa` endpoint and
you will see that the `taa_accepted` has changed from `null` to the details of the acceptance, showing the mechanism and time.

Accepting the TAA on the Sovrin MainNet isn't enough to give you permission to write, so we'll stop here. However we hope
the point has been made about how you can automate in your controller acceptance of the TAA.

## Takeaways

We've shown how the TAA works on an Indy ledger and how you can use the Aries Cloud Agent Python to accept the TAA as part of
your controller application. If you are using [VON-Network](https://github.com/bcgov/von-network) for development, there is no
active TAA. However, you can activate a TAA by using the `--taa-sample` option on the `./manage start...` command. Using that, your
code will be forced with the TAA from the start versus waiting to deal with a ledger that requires it.

That's it for this lab! Please return to the course.
