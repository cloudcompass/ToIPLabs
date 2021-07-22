<!----- Conversion time: 0.55 seconds.


Using this Markdown file:

1. Cut and paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β18
* Sat Feb 22 2020 09:33:50 GMT-0800 (PST)
* Source doc: https://docs.google.com/a/cloudcompass.ca/open?id=1g_joUJvks8aeuM-JHx0MtvKsruFi2-_wQQ8m_O8DIx8
----->



# Lab: Agent Startup Options


## Overview

In this lab, we'll demonstrate how to see the current list of ACA-Py parameters for both the `provision` and `start` modes of operation.


## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:



*   [Running LFS173x Labs](RunningLabs.md)


## Instructions

For this lab, we are going to use [these instructions in the ACA-Py repository](https://github.com/hyperledger/aries-cloudagent-python/blob/master/DevReadMe.md#configuring-aca-py-command-line-parameters) to review the current set of command line parameters for ACA-Py. To prepare to run the lab, clone the ACA-Py github repo (locally or on Play with Docker):


```
git clone https://github.com/hyperledger/aries-cloudagent-python
cd aries-cloudagent-python

```


Because the list of ACA-Py start up parameters is evolving regularly, the documentation for the list is in code instead of in documentation. As such, rather than list the parameters here, or even in the ACA-Py repo, you must run ACA-Py commands to see the current list of parameters.

Use the instructions here in the ACA-Py repo to run an ACA-Py docker image and see the startup parameters. Here is an example of the first command to run:


```
scripts/run_docker --help

```


The other commands to run for this lab to see all of the command line parameters are provided in the ACA-Py document.


## Takeaways

By completing this lab, you now know how to find the current set of command line parameters you can use in starting an instance of ACA-Py. As you go through the output from ACA-Py, you should compare that with the material we covered about ACA-Py in the [edX LFS173x](https://www.edx.org/course/becoming-a-hyperledger-aries-developer) course.

While this lab and the command line parameters reviewed are specific to ACA-Py, the concepts are more or less the same across all other Aries agent frameworks. The mechanism (command line parameters) and the precise list may vary in different frameworks, but some configuration mechanism must be available, and some set of configurable options must be available in each.

In later labs, we'll point out where in code the ACA-Py is started to see the command line parameters in effect for that agent instance.

That's it for this lab! Please return to the course.


<!-- Docs to Markdown version 1.0β18 -->
