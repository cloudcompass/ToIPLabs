# Lab: Aries Agent Test Harness Mobile Backchannel

## Overview

In this lab, we'll demonstrate how to test an Aries mobile wallet app on your phone with other Aries agents or frameworks using the Aries Agent Test Harness.
With this capability, you can test wallet apps you download from the mobile App Stores, and mobile wallet apps that you are developing and have loaded onto
your phone.

## How to Run

This lab can only be run locally with Docker, git and a bash shell. For general instructions for each, see the following:

* [Running LFS173x Labs](RunningLabs.md#running-on-docker-locally)

## Instructions

To prepare to run the lab, clone the Aries Agent Test Harness github repo (locally or on Play with Docker):

``` bash
git clone https://github.com/hyperledger/aries-agent-test-harness
cd aries-agent-test-harness

```

One your repository clone is ready, run the lab by following [these instructions in the Aries Agent Test Harness repository](https://github.com/hyperledger/aries-agent-test-harness/blob/main/MOBILE_AGENT_TESTING.md).

## Takeaways

Interoperability testing a mobile app like an Aries wallet is a pain! By using the Aries Agent Test Harness (AATH), we can run a whole lot of tests in a short time span, and we can test
the wallet against each of the Test Agents that have been included in AATH. As noted in the instructions document, it's not perfect as we still have to do a lot of manual QR code
scanning and responding to prompts on the phone. On the other hand, it's a lot better to run these tests regularly, as you go, versus waiting to hear from your customers that things
are not working with some production Aries apps!

That's it for this lab! Please return to the course.
