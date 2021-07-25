<!----- Conversion time: 0.461 seconds.


Using this Markdown file:

1. Cut and paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β18
* Sat Feb 22 2020 09:09:26 GMT-0800 (PST)
* Source doc: https://docs.google.com/a/cloudcompass.ca/open?id=1frEXG47NBDXQ8Bq55j10v1eOc8RhcbFw9Bg999Ioi4k
----->



# Lab: Using a Mediator


## Overview

In this lab, show a script running two ACA-Py-based agents interacting while one of them is using a mediator. We’ll be running a version of the Alice-Faber demo that is used for performance testing.


## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:



*   [Running LFS173x Labs](RunningLabs.md)


## Instructions

For this lab, you will need just a single terminal session. As with many of the other labs, clone the ACA-Py repo in the terminal session on Play with Docker or locally:


```
git clone https://github.com/hyperledger/aries-cloudagent-python
cd aries-cloudagent-python/demo

```


The performance demonstration runs an instance of Alice and Faber, and has Faber issue a number of credentials to Alice, one after another. Then, each agent publishes timing information about the calls executed and the time taken for those calls. Optionally, you can run the test with a mediator, which is what we’ll do first. To run the test execute this command:


```
LEDGER_URL=http://greenlight.bcovrin.vonx.io ./run_demo performance ---mediation --timing --count 100

```


After the run, review the timing output to see both the counts of the controller actions executed and the cumulative time taken for each action. As you scan the numbers, think about how controllers work and the number of actions that were executed. Do those counts make sense, given the number of credentials issued/received? Do the timings make sense? Note the actions that are especially slow. Think about why they would be slow. Likely it's because of the underlying cryptographic actions that are being executed. Notice as well that the total time taken to run the test is less the cumulative time for all the actions. Why? It’s because Faber is issuing multiple credentials in parallel—not waiting for Alice to respond to one before starting the next.

If you are interested, you can run the tests with a different number of credential issuances (by changing the `--count` number) and without the mediator (by removing the `--mediation` parameter). The latter change will show you the impact of the mediator.


### Navigating the Code

As we did with the Faber and Alice code, let’s take a quick look at the code for this demo, focusing on the impact of the router in the configuration. The code for the demo is in [performance.py](https://github.com/hyperledger/aries-cloudagent-python/blob/master/demo/runners/performance.py). You’ll see it is much like the Alice and Faber code, but with all three controllers run from the same script.

The main thing to note is the minimal impact of the mediator (router) on the code. Scanning the script we can find where the use of the router impacts the code—the places we see `if mediation` constructs:



*   Instantiating the router (mediator) controller - [line](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/performance.py#L237)
*   Starting the router ACA-Py process - line 245
*   Having Alice’s agent connect with the router agent - line 256
*   Having Alice’s agent add the router key data when connecting to Faber - line 263

After that, the Faber and Alice controllers don’t do anything differently—the rest of the controller code is the same with or without the mediator. Thus, Faber controller is unchanged, while the Alice controller has just two changes to account for the use of a mediator. Faber’s ACA-Py instance does behave differently (wrapping the message for Alice twice, and sending to the mediator), but that is invisible to the Faber controller. Likewise, Alice’s ACA-Py instance receives messages from the mediator, but again, that’s invisible to Alice’s controller.

The underlying message? Adding in mediators has a small impact on the controller that is going to use the mediator, but has no impact on anything else. Routing with mediators is handled at the messaging envelope protocol layer (DIDComm) without affecting the higher level Aries protocols.


## Takeaways

The key takeaway from this lab is how mediators can be integrated into agent-to-agent scenarios with minimal impact to the agents code. There is no impact on the controllers of agents connecting to an agent with a mediator. For an agent using a mediator, there is a little bit of effort in connecting to the mediator, but after that is done, the rest of the controller operations “just work” with the mediator in place.

Some of you will be disappointed that this lab does not include a mobile agent (or at least a simulated one) and a mediator for that mobile agent. We are too! To this point in the evolution of Aries, the mobile agent mediators that have been built have not been open source, so we have no good examples to share. That’s changing rapidly, and if we find a good mobile agent and mediator example, we’ll update this lab. Interested in contributing a mediator demo to one of the Aries repos?  Let us know!

That's it for this lab! Please return to the course.


<!-- Docs to Markdown version 1.0β18 -->
