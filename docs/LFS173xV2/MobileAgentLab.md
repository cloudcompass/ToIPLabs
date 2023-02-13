# Lab: Getting Started with the Aries Bifold Wallet

## Overview

In this lab, we'll take a look [Aries
Bifold](https://github.com/hyperledger/aries-mobile-agent-react-native), a
complete, open source Aries mobile wallet that you or your organization can
deploy today.

## How to Run

In this lab we’ll just take you to a couple of places that provide getting started details for using Aries Bifold and you can decide which you want to follow. In
both cases, you will need to install (if necessary) an Android simulator. iOS development and testing is of course, but requires a Mac and more setup, hence the
"Android first" approach.

## Instructions

We have two suggestions for setting up a getting started development of an Aries Bifold mobile wallet--Aries Bifold itself, or an open source, downstream implementation of
Aries Bifold, the [BC Wallet](https://github.com/bcgov/bc-wallet-mobile). Your choice depends on what you want to get out of the
exercise. Take a read through both sections and take your pick.

If you want to help the community (and build up your reputation!), we recommend
creating a GitHub issue, or better, doing a pull request, noting corrections you
find in the installation instructions based on your experience. You will be
thanked!!

As well, feel free to post an issue or PR to the [repo containing these
labs](https://github.com/cloudcompass/ToIPLabs) with updates to the information
here.

### Aries Mobile Agent React Native / Aries Bifold

The installation instructions for running a development instance of Aries Bifold can be found [here](https://github.com/hyperledger/aries-mobile-agent-react-native#install),
in the repository's README. As things are changing fast with Aries Bifold, that should have the latest information, so we won't repeat the details here. The instructions
as of last check (February, 2023) are not as complete as you will find with the BC Wallet, so it might be a bit tougher for those lacking mobile experience. On your first
pass, we would recommend skipping the iOS steps.

There is also a video linked in the README that provides a demonstration of a
user deploying an Aries Cloud Agent Python mediator and running an instance of
Aries Bifold connecting to another Agent.

### The BC Wallet

The installation instructions for running a development instance of BC Wallet
can be found in the [Developers
Guide](https://github.com/bcgov/bc-wallet-mobile/blob/main/DEVELOPER.md). BC
Wallet is built on top of Aries Bifold, and the wallet's build process merges
the code from the two repositories in building the apps. The vast majority of
the code in the BC Wallet is from Aries Bifold, so though you are using the
downstream BC Wallet, most of the capabilities are the same as in Aries Bifold
itself. If you are planning on creating your own wallet, it is not a bad tactic
to copy (not fork) the current state of the BC Wallet repository and then update
that code to make it your own. Much of the code is configuration data and
content specific to BC Gov that will be relatively easy to identify and update.

A reason for using the BC Wallet repository for this lab rather than using Aries
Bifold directly is that of this writing (February 2023), the instructions for the
BC Wallet go into more detail and so are easier to follow.

## Takeaways

Since the lab does not have any specific guidance on what to do, the only
takeaway is the experience gained as a developer in setting up to run an Aries
mobile wallet. Aries Bifold is evolving rapidly due to its many contributors. If
you are interested in creating your own spin on an Aries wallet, its a great
place to get started.

That's it for this lab! Please return to the course.
