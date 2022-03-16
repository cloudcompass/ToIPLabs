# Lab: Using a Mediator

## Overview

In this lab, show a script running two ACA-Py-based agents interacting while one of them is using a mediator. We’ll be running a version of the Alice-Faber demo that is used for performance testing.

## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:

- [Running LFS173x Labs](RunningLabs.md)

## Instructions

For this lab, you will need just a single terminal session. As with many of the other labs, clone the ACA-Py repo in the terminal session on Play with Docker or locally:

```bash
git clone https://github.com/hyperledger/aries-cloudagent-python
cd aries-cloudagent-python/demo

```

The performance demonstration runs an instance of Alice and Faber, and has Faber issue a number of credentials to Alice, one after another. Then, each agent publishes timing information about the calls executed and the time taken for those calls. Optionally, you can run the test with a mediator, which is what we’ll do first. To run the test execute this command:

```bash
LEDGER_URL=http://dev.greenlight.bcovrin.vonx.io ./run_demo performance --mediation --timing --count 100

```

Watch the terminal output to see all that is going on, including all the agents (Faber, Alice and the mediators) starting up and connecting. A lot going on! You'll see how little extra code is below.

After the run, review the timing output to see both the counts of the controller actions executed and the cumulative time taken for each action. As you scan the numbers, think about how controllers work and the number of actions that were executed. Do those counts make sense, given the number of credentials issued/received? Do the timings make sense? Note the actions that are especially slow. Think about why they would be slow. Likely it's because of the underlying cryptographic actions that are being executed. Notice as well that the total time taken to run the test is less the cumulative time for all the actions. Why? It’s because Faber is issuing multiple credentials in parallel—not waiting for Alice to respond to one before starting the next.

If you are interested, you can run the tests with a different number of credential issuances (by changing the `--count` number) and without the mediator (by removing the `--mediation` parameter). The latter change will show you the impact of the mediator (spoiler alert -- not much!)

By the way, in the progress bar, how come the "Receiving credentials" bar moves ahead of the "Issuing credentials" bar?

### Navigating the Code

As we did with the Faber and Alice code, let’s take a quick look at the code for this demo, focusing on the impact of the router in the configuration. The code for the demo is in [performance.py](https://github.com/hyperledger/aries-cloudagent-python/blob/master/demo/runners/performance.py). You’ll see it is much like the Alice and Faber code, but with all three controllers run from the same script.

The main thing to note is the minimal impact of the mediator (router) on the controller code. Scanning the script we can find where the use of the router impacts the code—the places we see `if mediation` constructs:

- Instantiating the mediators for Alice and Faber controller - [if needed](https://github.com/hyperledger/aries-cloudagent-python/blob/d78d4ea483e76c8033141e3c6c8e1a68e3a72096/demo/runners/performance.py#L310)
- Having Alice’s agent connect to their mediator agent - line 342
- Having Faber;s agent connect to their mediator agent - line 345

After that, the Faber and Alice controllers don’t do anything differently—the rest of the controller code is the same with or without the mediator.  The agents' ACA-Py instances do behave differently (wrapping the messages sent twice, and sending to the mediator), but that is invisible to the controllers. Likewise, the agent instances receive messages from the mediator, but again, that’s invisible to controller. Inspecting the demo "performance" code (search for "mediation"), you'll see the only other references relate to the timings of the runs.

The mediator agent itself is a little bit more substantive (although not much!), but a controller writer doesn't (usually) need to write that code -- they just deploy (or use) a mediator as a dependency.

- The mediator being used here is defined [here in the base agent class](https://github.com/hyperledger/aries-cloudagent-python/blob/d78d4ea483e76c8033141e3c6c8e1a68e3a72096/demo/runners/support/agent.py#L996)
- Alice and Faber are calling [this method](https://github.com/hyperledger/aries-cloudagent-python/blob/d78d4ea483e76c8033141e3c6c8e1a68e3a72096/demo/runners/support/agent.py#L1049) to use the instantiated mediator.

The underlying message? Adding in mediators has a small impact on the controller that is going to use the mediator, but has no impact on anything else. Routing with mediators is handled at the messaging envelope protocol layer (DIDComm) without affecting the higher level Aries protocols.

## Takeaways

The key takeaway from this lab is how mediators can be integrated into agent-to-agent scenarios with minimal impact to the agent controller code. There is no impact on the controllers of agents connecting to an agent with a mediator. For an agent using a mediator, there is a little bit of effort in connecting to the mediator, but after that is done, the rest of the controller operations “just work” with the mediator in place.

Oh, and about the progress bar question. If you look at the "Issue Credential" protocol ([RFC 0453 Issue Credential V2](https://github.com/hyperledger/aries-rfcs/tree/master/features/0453-issue-credential-v2)), the holder receiving the credential sends an "Ack" message back to the Issuer after receiving the credential, so it completes the protocol before the Issuer, who has to wait until the "Ack" messages is received and processed.

That's it for this lab! Please return to the course.
