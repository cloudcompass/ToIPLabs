# Lab: ACA-Py Startup Parameters

## Overview

In this lab, we'll demonstrate how to see the current list of ACA-Py parameters for both the `provision` and `start` modes of operation.

## How to Run

This lab can be run with locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:

* [Running LFS173x Labs](RunningLabs.md)

## Instructions

For this lab, we are going to use the instructions in the ACA-Py documentation to review the current set of command line parameters for ACA-Py. To prepare to run the lab, clone the ACA-Py github repo (locally or on Play with Docker):

```
github clone https://github.com/hyperledger/aries-cloudagent-python
cd aries-cloudagent-python
```

Because the list of ACA-Py start up parameters is evolving regularly, the documentation for the list is in code instead of in documentation. As such, rather than list the parameters here, or even in the ACA-Py repo, you must run ACA-Py commands to see the current full list of parameters.

Use the instructions here in the ACA-Py repo to run an ACA-Py docker image and so see the startup parameters. Here is an example of the first command to run:

```
./run_docker help
```

The other commands to run for this lab to see all of the command line parameters are provided in the ACA-Py document.

## Takeaways

In completing this lab you now know how to find the current set of command line parameters you can use in starting an instance of ACA-Py. In reviewing the list, you should align the list with the groups of command line parameters with the information in the corresponding section of the LFS173x course.

While this lab and the command line parameters reviewed were specific to ACA-Py, the concepts are likely the same across all other Aries agent frameworks. The mechanism (command line parameters) and the precise list may vary in different frameworks, some mechanism must be available, and some set of configurations must be in each.

In later labs, we'll point out where in the code ACA-Py is invoked to see the command line parameters in effect for that agent instance.

That's if for this lab. Please return to the course.

<!---
## To Do:
- NTH: Add screencast
- Add link to instructions in ACA-Py to do this
- Add links to running on PWD vs. locally
- If needed, update the instructions in ACA-Py
-->