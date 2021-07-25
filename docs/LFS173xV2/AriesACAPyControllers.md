# Lab: Python Not For You?

## Overview

In this lab, we'll go through three examples of Web controllers for ACA-Py using three different tech stacks. The story will be the same--Alice, Faber and ACME--but this time instead of running on the command line, the agent UI will be in browser tabs. Instead of Python, the code is in Angular, .Net and NodeJS/Express. Enjoy the variety!

## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:

- [Running LFS173x Labs](RunningLabs.md)

## Instructions

This lab does not use the ACA-Py repo, but instead references it from the Hyperledger repo [Aries ACA-Py Controllers](https://github.com/hyperledger/aries-acapy-controllers). The lab uses docker-compose to start everything up, including the same Alice, Faber and Acme agents used in the earlier labs. The instructions for getting started with the code examples [are here](https://github.com/hyperledger/aries-acapy-controllers/tree/master/AliceFaberAcmeDemo). The instructions include a section called “Running Locally” about running on a local machine without Docker. As always, we recommend not doing that the first time through, so you get the benefit of the demo without battling through getting everything installed and working on your specific machine configuration.

## Takeaways

Same old story, same old ACA-Py, brand new controllers. With this demo, we get away from Python development, still perform the same actions, but in other tech stacks. And, we (finally!) get away from the command line and provide a browser-based interface.

As we’ve mentioned (too often, we’re sure), the biggest thing you should notice is that controller development is very much like web development:

- Loop:
  - Wait for an event
  - Determine what to do about the event
  - Optionally—send a request in response to the event

That's it for this lab! Please return to the course.
