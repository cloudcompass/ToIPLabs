# Hyperledger Indy, Aries and Ursa Demonstrations

Welcome to the demonstration section of the Linux Foundation's edX course
[LFS172x, Introduction to Hyperledger Self Sovereign Identity Blockchain
Solutions](https://www.edx.org/course/identity-in-hyperledger-aries-indy-and-ursa).
In this section we have several demonstrations of Indy, Aries, AnonCreds and Ursa
technology.

## Mobile Wallet Demonstration

We'll start with downloading a published Aries mobile wallet from one of the
mobile OS App stores. Then, we'll run through some guided use cases of receiving
some AnonCreds credentials into the wallet, and presenting them to accomplish
some business goal. The scenarios are built on a (very cool!) open source
verifiable credentials demo framework created by the team at [Animo
Solutions](https:animo.id). The [BC
Wallet](https://digital.gov.bc.ca/digital-trust/projects-and-initiatives/bc-wallet-technology-overview/)
team at the Government of British Columbia used the framework to build a
showcase for their digital wallet.

* To try the Government of British Columbia's BC Wallet Showcase, [click
  here](https://digital.gov.bc.ca/digital-trust/showcase).
* To try Animo's wallet demo with a couple of other wallets, [click
  here](https://demo.animo.id)!

Or, if you want--try them both!

## Web Agent Demonstration

In the second demonstration, we build and run some web-based Aries agents that
interact to help Alice get proof of her degree from Faber College in the form of
an AnonCreds verifiable credential, and then present the credential as part of a
job application at ACME Corp. This is getting a bit ahead of ourselves, but
Alice gets the job! This demo is pretty raw compared to the showcases in the
Mobile Wallet demonstration, but if you are interested in looking at code, the
Aries applications are simpler, making it easier to learn about what is
going on. Each of the three agents in the hands-on demo
are built using a different tech stacks so you can pick your favorite if you
want to dive in and see what's going on.

To see a short screencast of the demo, click
[here](https://youtu.be/5EA-jqkvn4I).

Here's how to run a similar demo yourself. This gets a bit technical, but if you
just follow the instructions (including a bit of copying and pasting), you will
be good to go. You can run this on your local machine (if you have a developer
setup) or you can use an online tool called "Play with Docker" to run it in a
browser--no local setup needed. You will need an account with Docker to use
"Play with Docker" though...we'll help you through that.

[Click here for some
guidance](https://github.com/cloudcompass/ToIPLabs/blob/main/docs/LFS173x/RunningLabs.md)
on setting up to run the demo in a browser with "Play with Docker"
(recommended!) or directly on your own machine.

Ready to go?  [Click here for
instructions](https://github.com/hyperledger/aries-acapy-controllers/tree/main/AliceFaberAcmeDemo)
on running the lab! Have fun!

That's it for the demos! Please return to the course.
