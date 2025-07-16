# Lab: Issuing, Holding, Proving and Verifying

## Overview

In this lab, we'll use a couple of demo services published by the Government of British Columbia (BCGov -- in Canada) that issue and verify credentials, using the [BC Wallet] mobile agent to hold and prove credentials.

[BC Wallet]: https://digital.gov.bc.ca/design/digital-trust/digital-credentials/bc-wallet/

## How to Run

There are no components for you to deploy on your own system for this lab as we are using services that have been deployed for everyone to use.

## Instructions

To start, we'll use the BCGov's [BC Wallet Showcase], a demonstration of receiving, holding, presenting and verifying verifiable credentials. Click over to that site and follow the instructions to complete the demo (or demos, if you want).

[BC Wallet Showcase]: https://digital.gov.bc.ca/digital-trust/showcase/

The second demo, [The ACA-Py and AnonCreds Workshop], uses a sandbox deployment of BCGov's [Traction] service. In this 20 minute tutorial, you will create an issuer/verifier instance in Traction, define a type of verifiable credential, and then both issue that credential to your wallet, and request a presentation using it. While the steps are easy, the tutorial exposes a little more of the "under-the-covers" activities than you can see in the Showcase. Developers can use this to start to plan out how they could integrate the issuing and verifying of verifiable credentials in their own products.

[Traction]: https://digital.gov.bc.ca/digital-trust/technical-resources/traction/
[The ACA-Py and AnonCreds Workshop]: https://aca-py.org/latest/demo/ACA-Py-Workshop/

## Takeaways

This is a demonstration of some of the current user experiences with verified credentials. As you go through the demonstration, think about how the process works: 

- What are the interactions to get a verifiable credential and to present a proof?  
- How are those interactions handled on the website and in the mobile agent?  
- What do you think of the user interface? How would a non-technical person do with that interface?  
- What would you do differently?

As an Aries developer, these are the things that you can affect! And, since all of the underlying code is published in the open and ready to deploy, you can use it to jumpstart your implementation.

That's it for this lab! Please return to the course.
