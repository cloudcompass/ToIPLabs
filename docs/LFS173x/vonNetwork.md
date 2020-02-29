<!----- Conversion time: 0.933 seconds.


Using this Markdown file:

1. Cut and paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β18
* Sat Feb 22 2020 09:21:05 GMT-0800 (PST)
* Source doc: https://docs.google.com/a/cloudcompass.ca/open?id=1yGLPXrwtqMwwYkHL6IWisMu0WCpf4nePKFm6jDWGjL8

WARNING:
You have 2 H1 headings. You may want to use the "H1 -> H2" option to demote all headings by one level.

----->

# Lab: Running a VON Network Instance


## Overview

In this lab you will run a VON Network instance and use it to create a DID, look at the genesis file, and review some transactions on the ledger.


## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:



*   [Running LFS173x Labs](RunningLabs.md)


## Instructions

For this lab, we are going to use guidance in the `von-network` repository to run a VON Network and look at the ledger. Follow the [instructions here](https://github.com/bcgov/von-network/blob/master/docs/UsingVONNetwork.md) to complete the lab.


## Takeaways

On completing this lab you should have seen how easy it is to run an Indy network locally, and what kinds of tools are helpful in seeing data on the ledger. The power of running the VON Network is that you are immediately benefiting from the experience of others in making it easy to run an Indy network for development.

The scripts in VON Network provides the same ledger configuration as the examples in the official [`indy-node`](https://github.com/hyperledger/indy-node) repo (four nodes, and the same trustee and stewards DID seeds). VON Network includes some extra tools, such as the ledger browser web server that helps you see the transactions on the ledger. As you do the more advanced labs in the course, remember how you can access these tools to see the additional transactions on the ledger.

When you are getting your development or proof of concept environments going, you will likely want to use the VON Network. The repo’s [README.md](https://github.com/bcgov/von-network/blob/master/README.md) contains additional information about deploying the VON Network in different environments, including on cloud platform (like AWS) VMs. It also provides guidance for using the command line interface (CLI) capabilities to connect to local and remote Indy networks (even Sovrin’s MainNet) to execute permitted commands against the ledger.

That's it for this lab! Please return to the course.

<!-- Docs to Markdown version 1.0β18 -->
