# Lab: Open Source Mobile Agent Projects

## Overview

In this lab, we'll take a look at the open source options to use as the foundation for an Aries Mobile Agent.

## How to Run

In this lab we’ll just connect you to the options and you can look at the information available for you to use in getting started with these mobile agents.

## Instructions

There are two Aries mobile wallet projects, and both have good "getting started"
documentation for building and deploying a wallet in a development environment.
There are a lot more prerequisites for mobile development, not the least of
which is setting up to run an instance of your developer wallet instance on your
physical phone. If you have not done mobile development before, be prepared!

### Aries Mobile Agent React Native / Aries Bifold

The installation instructions for running a development instance of Aries Bifold can be found [here](https://github.com/hyperledger/aries-mobile-agent-react-native#install),
in the repository's README. As things are changing fast with Aries Bifold, that will always have the latest information, so we won't repeat the details here. However, here is a
quick summary of what you will have to setup:

- Clone (or fork and clone) the [Aries Mobile Agent React Native repository](https://github.com/hyperledger/aries-mobile-agent-react-native)
- Install react native for your combination of development machine OS (Mac, Windows or Linux) and mobile OS (Android or iOS)
  - If you are targeting iOS, you must use a Mac
  - Once you have installed react native, you can skip past the example setup of a new project
- Setup a mediator for your development mobile wallet app
- Deploy the app on either a simulator or uploaded to your device
- Play!

There is a video linked in the README that provides a demonstration of a user deploying an Aries Cloud Agent Python mediator and running an instance of Aries Bifold connecting
to another Agent. If you want to help the community (and build up your reputation!), we recommend doing a pull request updating the installation instructions based on your experience,
and/or posting a video of using your instance of Aries Bifold.

As well, feel free to post an issue or PR to the [repo containing these labs](https://github.com/cloudcompass/ToIPLabs) with updates to the information here.

### Aries Mobile Agent Xamarin / Aries MAX

The installation instructions for running a development instance of Aries MAX can be found [here](https://github.com/hyperledger/aries-mobile-agent-xamarin),
in the repository's README. The instructions are not as detailed as with Aries Bifold, and we're looking to see if we can get some more guidance. It appears
that more knowledge of .NET Core is needed for running a simulator or creating a mobile instance of the wallet to load onto your device. There is a good
video on the site of the process that should help with getting started.

As the writing of this lab, there is active development happening with Aries MAX, but not as much as on Bifold. As such, unless you are a .NET developer,
we recommend focusing on Aries Bifold.  We'll update this information should the situation while this edX course is active.

## Takeaways

Since the lab does not have any specific guidance on what to do, the only takeaway is that there are some open source options for getting started in building an Aries Mobile Agent. As Aries open source mobile agent capabilities mature and getting started information becomes available, we’ll update this page.

That's it for this lab! Please return to the course.
