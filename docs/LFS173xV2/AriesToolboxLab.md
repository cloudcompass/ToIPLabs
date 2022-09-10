# Lab: The Aries Toolbox<!-- omit in toc -->

- [Overview](#overview)
- [How to Run](#how-to-run)
  - [Installing node and npm](#installing-node-and-npm)
- [Instructions](#instructions)
  - [Running Aries Toolbox](#running-aries-toolbox)
  - [Running ACA-Py Agents](#running-aca-py-agents)
  - [Things You Can Do](#things-you-can-do)
  - [Stopping the Aries Toolbox](#stopping-the-aries-toolbox)
- [Takeaways](#takeaways)

## Overview

In this lab, we'll show you how to start up the Aries Toolbox and connect it with a couple of ACA-Py agents. Oddly, instead of Alice and Faber, we’ll be using agents for Alice and Bob. But that’s OK, only a name has been changed—the concepts are the same!

## How to Run

Since Aries Toolbox is an [Electron](https://www.electronjs.org/) app, you must run at least part of this lab on your own system. The second element of this lab, the actual agents for Alice and Bob, can run on your local machine with Docker or
on Play-with-Docker as we've seen before.

### Installing node and npm

The need to run Aries Toolbox locally will add a new dependency to our list. To run this lab you need to have [nodejs](https://nodejs.org/) and [npm](https://www.npmjs.com/) (node package manager) installed. If you don’t have those installed on your system already, here is some guidance on installing them on different systems:

- To see if you have node already try running `node --version`. All good? Skip ahead!
- If you are on a Mac and use Homebrew, you can install node and npm with: `brew install node`
- If you are on Windows and use Chocolatey, you can install node and npm with: `choco install nodejs`
- If you are on Linux, you can do a comparable command with your package manager.

If you don't have any of those, you can first install `nvm` (node version manager) using the instructions [here](https://github.com/nvm-sh/nvm/blob/master/README.md#installing-and-updating). The instructions are long, but on MacOS, Windows (in a bash shell)
and Linux amounts to running the single `curl` (or `wget`) command, and follow the instructions printed at the end of the installation.

Once you have `nvm` running, run the command `nvm install node` and you will have node and npm installed.

Finally, run `node --version` to make sure you are good to go with node.

## Instructions

Please open up two terminals running bash, and we’ll start in the first. Note that, the first must be on a local machine with a window manager (e.g. Mac, Windows or a Linux Desktop), while the second can be wherever you have run the Docker labs in the past, including Play With Docker, if you want.

### Running Aries Toolbox

Get a local clone of the Aries Toolbox, build it and run it:

```bash
git clone https://github.com/hyperledger/aries-toolbox
cd aries-toolbox
npm i
npm run dev

```

If all goes well, you should have an Aries Toolbox running on your screen and a place to paste new invitations. If you have
the Toolbox previously, you might see other connections. If so, you can delete them to get back to a blank setup.

### Running ACA-Py Agents

In your second terminal, get a local clone of the Aries ACA-Py Plugins Toolbox repo and use docker-compose to start up Alice and Bob:

```bash
git clone https://github.com/hyperledger/aries-acapy-plugin-toolbox
cd aries-acapy-plugin-toolbox/demo
docker-compose -f docker-compose.alice-bob.yml up --build

```

If all goes well, you should see on the **terminal** information in a square box framed in colons (“:”) listing info about the agents for Alice and Bob, and below each, an invitation URLs, similar to the following:

```bash
agent-bob_1     | Invitation URL (Connections protocol):
agent-bob_1     | https://old-fox-20.loca.lt?...W1QWiJdfQ==
```

Find one of the invitation URLs, highlight (from `https: through to the end of the very long URL) and copy the text to your clipboard, paste it into the Aries Toolbox invitations field and click ‘Connect.’
You should see a new connection in the Aries Toolbox window. Click "Open" and a new window will open for the newly connected agent. Repeat for the second agent (you may have to scroll back a bit in your terminal window).

You should see a long menu in the left side menu of each agent. If you don't, although the agent did get a connection with the Toolbox, it is not running.
If that happens, you should stop (see instructions below) and start the Alice and Bob agents again.

OK, good, you have two Aries agents connected to the Toolbox.

### Things You Can Do

There are not currently a lot of instructions on what you can do with the Aries Toolbox, but here are a few ideas:

- Use the “Invitations” menu item in the Alice window to create and copy an invitation, and paste it into the appropriate field in the “Connections” menu item of Bob’s window. That should enable a connection between Alice and Bob.
- Find the DIDs that Alice and Bob are using for connections to each other and “Activate” those connections from the “Connections” menu item.
- Play around with the Credentials section. For example, have Alice create a schema and a credential definition and issue a credential to Bob. Further, have Alice request a proof request from Bob about that credential.
  - The Aries Toolbox uses the Sovrin BuilderNet network by default. To issue credentials, the issuer must:
    - Accept the Sovrin BuilderNet Transaction Author Agreement
    - Use the [Sovrin Self-Service](https://selfserve.sovrin.org/) to write an Endorser DID to the ledger.
- Create an invitation, display its QR code and scan it with one of the mobile wallet apps (one of those listed [here](../../GetWallet.md)).

We’ll keep monitoring the Aries Toolbox sites and if tutorials about the Aries Toolbox are posted, we’ll link to them from here.

### Stopping the Aries Toolbox

To stop the Aries Toolbox, go to one of the screens and choose the top menu item “File/Quit.” In the first terminal, you will be back at the command line, and you can exit.

To stop the ACA-Py agents, go to the second terminal and:

- Hit Ctrl-C to terminate the agents.
- To cleanup the docker sessions run:

  ``` bash
  docker-compose -f docker-compose.alice-bob.yml down

  ```

Exit out of the second terminal session.

## Takeaways

This lab shows one of the new tools created in the Aries community and a new approach to interacting with running agents. There will be more to come with the Aries Toolbox, so keep on it as it evolves!

That's it for this lab! Please return to the course.
