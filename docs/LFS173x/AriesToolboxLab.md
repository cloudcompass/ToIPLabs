<!----- Conversion time: 5.573 seconds.


Using this Markdown file:

1. Cut and paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β18
* Sat Feb 22 2020 09:39:39 GMT-0800 (PST)
* Source doc: https://docs.google.com/a/cloudcompass.ca/open?id=1jUeUK7cuANsiG3-Fxpqxf8THq9ZmTE4boy87wHWwcK4
----->



# Lab: The Aries Toolbox<!-- omit in toc -->

- [Overview](#overview)
- [How to Run](#how-to-run)
- [Instructions](#instructions)
  - [Running Aries Toolbox](#running-aries-toolbox)
  - [Running ACA-Py Agents](#running-aca-py-agents)
  - [Things You Can Do](#things-you-can-do)
  - [Stopping the Lab](#stopping-the-lab)
- [Takeaways](#takeaways)


## Overview

In this lab, we'll show you how to start up the Aries Toolbox and connect it with a couple of ACA-Py agents. Oddly, instead of Alice and Faber, we’ll be using agents for Alice and Bob. But that’s OK, only a name has been changed—the concepts are the same!


## How to Run

Since Aries Toolbox is an [Electron](https://www.electronjs.org/) app, you must run this lab on your own system—you can’t use Play with Docker.  We’ll still be using Docker for some ACA-Py agents that we’ll connect to the Aries Toolbox, but the Toolbox itself must be run on a local system.

The need to run Aries Toolbox locally will add a new dependency to our list. To run this lab you need to have [nodejs](https://nodejs.org/) and [npm](https://www.npmjs.com/) (node package manager) installed. If you don’t have those installed on your system already, follow the instructions [here](https://www.npmjs.com/get-npm) to install them.


## Instructions

Please open up two terminals running bash, and we’ll start in the first.


### Running Aries Toolbox

Get a local clone of the Aries Toolbox, build it and run it:


```
git clone https://github.com/hyperledger/aries-toolbox
cd aries-toolbox
npm i
npm run dev

```


If all goes well, you should have an Aries Toolbox running on your screen, with a link to Alice and Bob, and a place to paste new invitations. Since we are going to connect to new Alice and Bob Aries agent instances, delete the two you see on the screen, leaving just a place to paste invitations.


### Running ACA-Py Agents

Get a local clone of the Aries ACA-Py Plugins Toolbox repo and use docker-compose to start up Alice and Bob:


```
git clone https://github.com/hyperledger/aries-acapy-plugin-toolbox
cd aries-acapy-plugin-toolbox/demo
docker-compose -f docker-compose.alice-bob.yml up --build
```


If all goes well, you should see on the **terminal** information in a square box framed in colons (“:”) listing info about the agents for Alice and Bob, and below that, invitation URLs. In the version we're looking at, there are a lot of `Node is not a validator` error messages, which you can ignore, but that require you to scroll back a long way to find the first invitation.

Find one of the invitation URLs, highlight and copy the text to your clipboard, paste it into the Aries Toolbox invitations field and click ‘Connect.’ You should see a new connection in the Aries Toolbox window, and after you click "Open", a new window for the newly connected agent. Repeat for the second agent (you may have to scroll quite a way in your terminal window).

You should see a long menu in the left side menu of each agent. If you don't, although the agent did get a connection with the Toolbox, it is not running. If that happens, you should stop (see instructions below) and start the Alice and Bob agents again.

OK, good, you have two Aries agents connected to the Toolbox.


### Things You Can Do

There are not currently a lot of instructions on what you can do with the Aries Toolbox, but here are a few ideas:



*   Use the “Invitations” menu item in the Alice window to create and copy an invitation, and paste it into the appropriate field in the “Connections” menu item of Bob’s window. That should enable a connection between Alice and Bob.
*   Find the DIDs that Alice and Bob are using for connections to each other and “Activate” those connections from the “Connections” menu item.
*   Play around with the Credentials section. For example, have Alice create a schema and a credential definition and issue a credential to Bob. Further, have Alice request a proof request from Bob about that credential.

We’ll keep monitoring the Aries Toolbox sites and if tutorials about the Aries Toolbox are posted, we’ll link to them from here.


### Stopping the Lab

To stop the Aries Toolbox, go to one of the screens and choose the top menu item “File/Quit.” In the first terminal, you will be back at the command line, and you can exit.

To stop the ACA-Py agents, go to the second terminal and:




*   Hit Ctrl-C to terminate the agents.
*   To cleanup the docker sessions run:

        ```
        docker-compose -f docker-compose_alice_bob.yml down

        ```


Exit out of the second terminal session.


## Takeaways

This lab shows one of the new tools created in the Aries community and a new approach to interacting with running agents. There will be more to come with the Aries Toolbox, so keep on it as it evolves!

That's it for this lab! Please return to the course.


<!-- Docs to Markdown version 1.0β18 -->
