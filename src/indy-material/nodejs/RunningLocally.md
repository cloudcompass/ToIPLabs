# Hyperledger Indy, Aries, Ursa Demonstration: Running on Your Local Machine

The Hyperledger Indy Agent demo can be run [using just a browser](README.md). However, if you are more technically inclined, you can run it on your local machine. This document outlines the steps for running the demo on your local machine.

> **This demonstration is based on some early Indy Agent code that should *NOT* be used as the basis of new implementations or as a reference for implementing an agent. Since this demonstration was developed the Indy and Aries community has evolved the notion of Agents significantly and this code base has been abandoned. It is still a good demo for understanding how agents work on a superficial level -- the concepts of agents connecting and exchanging credentials. However, if you are interested in building on the latest Indy/Aries code, you should look at the [Aries project](https://github.com/hyperledger/aries), the [Aries Cloud Agent - Python](https://github.com/hyperledger/aries-cloudagent-python) and other interoperable components. If you are a developer (or wannabe), check out this [Becoming an Indy/Aries Developer](https://github.com/hyperledger/aries-cloudagent-python/tree/master/docs/GettingStartedAriesDev) guide.**

## **Prerequisite**

To run this Indy Agent demonstration on your local machine, you must have the following installed:

- Docker, including Docker Compose - Community Edition is fine.
  - If you do not already have Docker installed, open [this link](https://docs.docker.com/install/#supported-platforms) and then click the link for the installation instructions for your platform.
- git
  - [This link](https://www.linode.com/docs/development/version-control/how-to-install-git-on-linux-mac-and-windows/) provides installation instructions for Mac, Linux (including if you are running Linux using VirtualBox) and native Windows (without VirtualBox).

## Installing the Demonstration

To install the demonstration on your local machine, you need to clone the git repository. To do that:

1. Install the prerequisites listed above and make sure they are functioning on your system. To verify, open a terminal window and:
    1. Run `git --version`, which should return something like: git version 2.17.1
    2. Run `docker --version`, which should return something like: `Docker version 23.0.1, build a5ee5b1`
    3. Your version numbers should be the same or higher.
2. Open a terminal session and navigate to where you want to install the source code.

3. Run the command:

``` bash
    git clone https://github.com/cloudcompass/ToIPLabs
```

That will download the repository containing the source code onto your system.

4. Navigate to the location of the code by running the command:

``` bash
    cd src/indy-material/nodejs
```

## Starting the Demonstration

To run the demo:

1. Run the following command to build the components of the software:

```bash
./manage build
```

2. Run the command to bring up the demonstration components:

```
./manage up
```

It takes a while for the demo to start—lots of things are happening. The logs for all of the containers will display in the terminal window. Logs show the output of both the Blockchain ledger nodes communicating and the Indy agents starting up and communicating with the ledger.

Things to watch for as the demo starts up:

- You should periodically see things such as "Listening on port 3001", which indicates an agent is up and running.
- You should not see a stack trace error in the code—that would indicate a problem.
- You should not see any "Container exiting" messages, indicating containers not starting up properly.
- There should be 10 docker containers running. You can hit CTRL-C to exit the log viewer and run the command `docker ps` to see all of the containers running. Run `./manage logs` if you want to see the logs again.
- Once the output slows significantly and you only see messages from the ledger nodes (the containers running the ledger), everything should be working.

Access the ledger and agents in a web browser:

To go through the demonstration, open the following links in new browser tabs:

- [http://localhost:3000](http://localhost:3000/) for Alice
- [http://localhost:3002](http://localhost:3002/) for Faber College
- [http://localhost:3003](http://localhost:3003/) for Acme Corporation

If you click the links before the agent is active, you might get a `connection reset by peer` error messages. Monitor the logs and wait longer and then try again.

Once you have the demo started, this [Agent Demo Script](AgentDemoScript.md) guides you through the scenario of Alice using Hyperledger Indy to get her transcripts from Faber College and then using them to apply for a job with Acme Corp.

You can also open in a browser a ledger explorer:

- [http://localhost:9000](http://localhost:9000/)

Although we don't talk about them in the demo overview, there are two additional agents running that you can access:

- [http://localhost:3001](http://localhost:3001/) for Bob
- [http://localhost:3004](http://localhost:3004/) for Thrift Bank

## Stopping the Demo

To stop the demo, go to the terminal window where you ran `./manage up` command. If the logs are scrolling and/or you are not at the command prompt, hit Ctrl-C and you should be back at  command prompt. Run the command `./manage down`. You should see a list of the containers and a Done message as each stops. Run the command `docker ps` to confirm that all of the containers have stopped.
