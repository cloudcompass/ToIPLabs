# Hyperledger Indy, Aries, Ursa Agent Demonstration

This folder contains a demonstration of basic Hyperledger Indy and Aries Agents, which are built on the Ursa project. The agents provide a web browser interface to show establishing relationships between agents, issuing verifiable credentials, and proving claims from verifiable credentials.

> **This demonstration is based on some early Indy agent code that should *NOT* be used as the basis of new implementations or as a reference for implementing an agent. Since this demonstration was developed the Indy (and Aries) community has evolved the notion of Agents significantly and this code base has been abandoned. It is still a good demo for understanding how agents work on a superficial level&mdash;the concepts of agents connecting and exchanging credentials. However, if you are interested in building on the latest Indy/Aries code, you should look at the [Aries project](https://github.com/hyperledger/aries), the [Aries Cloud Agent - Python](https://github.com/hyperledger/aries-cloudagent-python) and other interoperable components. If you are a developer (or wannabe), check out this [Becoming an Indy/Aries Developer](https://github.com/hyperledger/aries-cloudagent-python/tree/master/docs/GettingStartedAriesDev) guide.**

- To learn more about Hyperledger Indy, see the [Indy project wiki](https://wiki.hyperledger.org/display/indy).
- To learn more about Hyperledger Aries, see the [Aries project wiki](https://wiki.hyperledger.org/display/aries).
- To learn more about Hyperledger Ursa, see the [Ursa project wiki](https://wiki.hyperledger.org/display/ursa)

This demo is used as a demonstration for those taking the Linux Foundations's edX LF172x course, *Introduction to Hyperledger Sovereign Identity Blockchain Solutions: Indy, Aries and Ursa*.

[Click here](https://youtu.be/5EA-jqkvn4I) to view a short screencast of the demo.

## Prerequisites

The only prequisite (other than a browser) is an account with [Docker Hub](https://hub.docker.com). Docker Hub is the "Play Store" for the [Docker](https://docker.com) ecosystem.

## Installing the Demonstration

Go to the [Play with Docker](https://labs.play-with-docker.com/) and (if necessary) login. This site is operated by Docker to support developers learning about Docker.

> If you want to learn more about the `Play with Docker` environment, look at the [About](https://training.play-with-docker.com/about/) and the Docker related tutorials at the Docker Labs [Training Site](https://training.play-with-docker.com).

Click the "Start" button to start a Docker sandbox you can use to run the demo, and then click the `+Add an Instance` link to start a terminal in your browser. Within the terminal that is visible in your browser, run the following commands:

``` bash
git clone https://github.com/cloudcompass/ToIPLabs
cd ToIPLabs/src/indy-material/nodejs

```

> **Tip**: To paste text in the terminal window, right-click on the window and choose `paste`

## Starting the Demonstration

The steps for running the demonstration are:

- Run the command `./manage build` to build the components of the software
- Run the command `./manage up` to run the components

It takes a while for the demo to start&mdash;lots of things are happening. The logs for all of the containers will display in the terminal window. Logs show the output of both the Blockchain Ledger nodes communicating and the Indy agents starting up and communicating with the ledger.

Things to watch for as the demo starts up:

- You should periodically see things like "Listening on port 3001," which indicates an Agent is up and running.
- You should **not** see a stack trace error in the code&mdash;that would indicate a problem.
- You should **not** see any "Container exiting" messages, indicating containers not starting up properly.
- There should be 10 docker containers running. You can hit `ctrl-c` to exit the log viewer and run the command `docker ps` to see all of the containers running.
  - To get back to seeing the scrolling logs, run `./manage logs`.
- Once the output slows significantly and you only see messages from the nodes (the containers running the ledger), everything should be working.

### Accessing the ledger and agents in a web browser:

As the demo starts up, a series of four digit numbers will appear above the terminal. Those are the exposed ports of the running containers and the numbers are links to start a browser tab accessing that port.

To go through the demonstration, click the following numbers from the list:

- **3000** for Alice
- **3002** for Faber College
- **3003** for Acme Corporation

If you click the links before the agent is active, you might get a `Connection reset by peer` error messages. Monitor the logs and wait longer and then try again.

The instructions for walking through the demonstration script are here: [Agent Demo Script](AgentDemoScript.md).

You can also open the Blockchain Ledger Explorer:

- **9000** for the Ledger Explorer

Although we don't talk about them in the demo overview, there are two additional agents running that you can access:

- **3001** for Bob
- **3004** for Thrift Bank

> The remainder of the numbers, (ports 9701-9708) are the ports to the Blockchain Ledger nodes, two per node.

## Stopping the Demo

To stop the demo, go to the browser tab where you ran `docker compose up`, click the red `Close Session` button on the left and close the browser tab. Note that if you don't close the session or the tab, the terminal session will expire 4 hours after you started it.

## Running the Demo on Your Own Machine

If you'd like to run the demo locally, on your own machine, see the instructions [here](RunningLocally.md).

## Credits

The code for this demonstration was initially written by Spencer Holman and Matthew Hailstone of Brigham Young University. Carol Howard created the documentation for the demonstration.