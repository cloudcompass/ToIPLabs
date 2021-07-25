# Lab: Agent Startup Options

## Overview

In this lab, we'll demonstrate how to see the current list of ACA-Py parameters for both the `provision` and `start` modes of operation.

## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:

- [Running LFS173x Labs](RunningLabs.md)

## Instructions

For this lab, we are going to use [these instructions in the ACA-Py repository](https://github.com/hyperledger/aries-cloudagent-python/blob/master/DevReadMe.md#configuring-aca-py-command-line-parameters) to review the current set of command line parameters for ACA-Py. To prepare to run the lab, clone the ACA-Py github repo (locally or on Play with Docker):

```bash
git clone https://github.com/hyperledger/aries-cloudagent-python
cd aries-cloudagent-python

```

Because the list of ACA-Py start up parameters is evolving regularly, the documentation for the list is in code instead of in documentation. As such, rather than list the parameters here, or even in the ACA-Py repo, you must run ACA-Py commands to see the current list of parameters.

Use the instructions here in the ACA-Py repo to run an ACA-Py docker image and see the startup parameters. Here is an example of the first command to run, to see the version of ACA-Py you are running.

```bash
scripts/run_docker --version

```

When you run that, you will see that an ACA-Py docker image is first built, which could take a while on the first run. On subsequent runs, the build step will be pretty quick.

To see the options for `provision` and `start`, use these commands:

```bash
scripts/run_docker provision --help

```

```bash
scripts/run_docker start --help

```

There are a lot of options! Note the environment variables that you can use as an alternative to using the command line options. And don't forget
about using an ACA-Py config YAML file. So many options for options!

One more thing for those that might be interested. To see how to build ACA-Py, we can take a look at the dockerfile used by the `run_docker` script by running this command:

```bash
cat docker/Dockerfile.run

```

## Takeaways

By completing this lab, you now know how to find the current set of command line parameters you can use in starting an instance of ACA-Py. As you go through the output from ACA-Py, you should compare that with the material we covered about ACA-Py in the [edX LFS173x](https://www.edx.org/course/becoming-a-hyperledger-aries-developer) course.

While this lab and the command line parameters reviewed are specific to ACA-Py, the concepts are more or less the same across all other Aries agent frameworks. The mechanism (command line parameters) and the precise list may vary in different frameworks, but some configuration mechanism must be available, and some set of configurable options must be available in each.

In later labs, we'll point out where in code the ACA-Py is started to see the command line parameters in effect for that agent instance.

That's it for this lab! Please return to the course.
