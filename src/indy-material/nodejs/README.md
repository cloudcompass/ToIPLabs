# Hyperledger Indy, Aries, Ursa Agent Demonstration

NOTE: This folder contains some old code that is no longer maintained that was an early version of an "Indy Agent" -- a think that pre-dates the Aries Agents we are using today. An [old README](oldREADME.md) exists for historical purposes, but this code should not be used, and the demo does not run because of old dependencies no longer available on the Internet. Instead, we're going to use a more modern
version of the lab based on Aries Cloud Agent Python and some web controllers built on different stacks that demonstrate the same principles.

## Overview

In this lab, we'll go through three examples of Web controllers for Aries Cloud Agent Python (ACA-Py) using three different tech stacks. The story will be about Alice getting a verifiable credential about the degree she received from Faber College (the Issuer) and Alice presenting data from the credential to ACME where she is applying for a job. All of the agent interfaces will be in browser tabs. The code instances are in Angular, .Net and NodeJS/Express.

## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:

- [Running LFS173x Labs](../../../docs/LFS173x/RunningLabs.md)

## Instructions

This lab does not use the ACA-Py repo, but instead references ACA-Py from the Hyperledger repo [Aries ACA-Py Controllers](https://github.com/hyperledger/aries-acapy-controllers). The lab uses docker-compose to start everything up, including the same Alice, Faber and Acme agents. The instructions for getting started with the code examples [are here](https://github.com/hyperledger/aries-acapy-controllers/tree/main/AliceFaberAcmeDemo). The instructions include a section called “Running Locally” about running on a local machine without Docker. As always, we recommend not doing that the first time through, so you get the benefit of the demo without battling through getting everything installed and working on your specific machine configuration.

## Takeaways

With this demo, we demonstrate a Web-based user interface for exchanging credentials. The interface is still pretty raw, but it gives you an idea of what is possible. For the developers taking the course, the code is current and demonstrates agents using three different tech stacks.

That's it for this lab! Please return to the course.
