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

# **Lab: Running a VON Network Instance**


## **Overview**

In this lab you will run a VON Network instance and use it to create a DID, look at the genesis file, and review some transactions on the ledger.


## **How to Run**

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:



*   [Running LFS173x Labs](RunningLabs.md)


## **Instructions**

For this lab, we are going to use guidance in the `von-network` repository to run a VON Network and look at the ledger. To prepare to run the lab, clone the `von-network` GitHub repo (locally or on Play with Docker):


```
git clone https://github.com/hyperledger/von-network
cd von-network
```


Follow the [instructions here](https://github.com/bcgov/von-network/tutorial.md) to complete the lab.


## **Takeaways**

On completing this lab you should have seen how easy it is to run an Indy network locally, and what kinds of tools are helpful in seeing data on the ledger. The power of running the VON Network is that you are immediately benefiting from the experience of others in making it easy to run an Indy network for development. \
 \
The scripts in VON Network provides the same ledger configuration as the examples in the official <code>[indy-node](https://github.com/hyperledger/indy-node)</code> repo (four nodes, and the same trustee and stewards DID seeds), but include some extra tools, such as the ledger browser web server that helps you see the transactions on the ledger. As you do the more advanced labs in the course, remember how you can access these tools to see the additional transactions on the ledger.

When you are getting your development or proof of concept environments going, you will likely want to use the VON Network. The repo’s Readme contains additional information about deploying the VON Network in different environments, including on cloud platform (like AWS) VMs. It also provides guidance for using the command line interface (CLI) capabilities to connect to local and remote Indy networks (even Sovrin’s MainNet) to execute permitted commands against the ledger.

That's it for this lab! Please return to the course.

———————————-


# VON Network Tutorial

This tutorial provides some guidance for newcomers on what you can do with a running VON Network instance. If you got here as part of the edX LF173x course, skip the prerequisites as you’ve seen them before.


## Prerequisites

The instructions cover running the demo on docker locally or on Play with Docker, and you have prerequisites for running demos in these environments.

If you haven’t done so already, get to a `bash` command line and clone the `von-network `repo:


```
github clone https://github.com/hyperledger/von-network
cd von-network
```



## Building and Starting

Begin by building the images for the VON Network and then starting your network:


```
./manage build
./manage start
```


The `./manage` bash script simplifies the process of running the VON Network, providing the common entry points that you need to use. It also provides a number of environment variables you can use to customize the running of the script.

The images are built using Docker scripts that encapsulate the steps to create `indy-node` from scratch, starting with base Docker images that contain all necessary prerequisites. The base images are created once per `indy-node` release, so that the entire community can benefit from that work.

To see what you can do with the script, after your network is running (from the commands above), hit Ctrl-C in the terminal to get back to the command prompt. Your network is still running. Run the command with no arguments to see the usage info for the script.


```
./manage
```


If you want to get back to seeing the logging data from the nodes, run with the “logs” parameter:


```
./manage logs
```



## Browsing the Ledger

Once the ledger is running, you can see the ledger by going to the web server running on port 9000. On localhost, that means going to [https://localhost:9000](https://localhost:9000). From there you can:



*   See the status of the nodes of the network.
*   Look at the genesis file for the network.
*   Create a DID.
*   Browser the three ledgers that make up an Indy network:
    *   The Domain ledger, where the DIDs, schema, etc. reside.
    *   The Pool ledger, where the set of nodes on the network are tracked.
    *   The Config ledger, where changes to the network configuration are tracked.


## Viewing Transactions

Click the “Domain Ledger” link from the main menu to see the transactions on the ledger. On a brand new ledger, there will be five transactions, the first for the trustee DID and the next four for each of the stewards on the network. The stewards are the operators of the four nodes operating on the network.

**Note:** _You can search on the ledger by transaction type or by the text in the transactions. For example, in the “Filter,” type “trustee” and hit enter. The four “steward” transactions will be hidden and you will see just one transaction. Not too useful with only five transactions on the ledger, but really useful when there are 100,000!_


## Creating a DID

To create a DID, go to the Ledger Browser (at port 9000) and find the “Authenticate a New DID” section. There are various options, but we’ll do the simplest case:



1. Make sure that “Register from Seed” is selected.
2. Type your first name in the “Wallet Seed” field, and your full name in the “Alias” field.
3. Click “Register DID.”

You should get a response back with the details of the newly created DID.



1. Next, go to the Domain Ledger and find the transaction. Put the alias you used for the DID in the filter to see that you can search for the DID.


## Viewing the Genesis File

From the main menu of the Ledger Browser, click on the “Genesis Transaction” link to see the genesis file for the network. When running a VON Network instance with the Ledger Browser, you always get the genesis file from the /genesis endpoint—which is something we can use as a startup parameter for an Aries agent. 

If you want to see the connection between the genesis file and the ledger entries, copy and paste the “from” item value from one of the lines of the genesis file (e.g. “`TWwCRQRZ2ZHMJFn9TzLp7W`”), and then go back to the Domain Ledger and search for a transaction with that same ID.

**Note:** _The DIDs in the genesis file (the “from” values) are the same for any instance of an indy sandbox ledger, hence the ID in the previous paragraph. Once you are using production (or production-like) ledgers, the contents of the files will be different._

Another thing to notice about the ledger file is the IP addresses for the ledger nodes. Since the nodes are running in a Docker container, the IP address is that of the Docker container, not localhost. One of the benefits of using the VON Network is that it takes care of details like that, making sure that the genesis file is always accurate for the network that is running.


## Using the CLI

The VON Network provides a way to get to an Indy command line interface (CLI). To get to the Indy CLI for the network, get to the command prompt (using Ctrl-C if necessary) and run the command:


```
./manage indy-cli
```


Run the “help” command to see what you can do, and “exit” to get out of the CLI session.

We won’t go into the Indy CLI here, but it has powerful capability that you can use to create scripts for configuring an Indy network and adding objects to the ledger. If you find any Indy CLI tutorials on other sites, you can run them using this mechanism, without any of the bother of getting everything running before you start the CLI.


## Stopping and Removing a VON Network

To stop and delete a running VON Network, get to a command line prompt (using Ctrl-C if necessary), and then run the command:


```
./manage down
```


You would normally do that when you have done some development, completed your testing and want to start again fresh.

If you want to stop the network WITHOUT deleting the data on the ledger, use the following command: 


```
./manage stop
```


You can restart the ledger by running the normal command for starting the network:


```
./manage start
```


Make sure that you keep your agent storage and ledger in sync. If you delete/reset one, delete/reset the other.


<!-- Docs to Markdown version 1.0β18 -->
