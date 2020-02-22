<!----- Conversion time: 1.558 seconds.


Using this Markdown file:

1. Cut and paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β18
* Sat Feb 22 2020 09:27:30 GMT-0800 (PST)
* Source doc: https://docs.google.com/a/cloudcompass.ca/open?id=150AoXQ4beWsXFJ7EBEBR9Y6QUvP3ifBn66gL3TE8_0o
----->



# **Lab: Agents Connecting**<!-- omit in toc -->

- [**Overview**](#overview)
- [**How to Run**](#how-to-run)
- [**Instructions**](#instructions)
- [**Navigating the Code**](#navigating-the-code)
  - [Faber Controller](#faber-controller)
    - [Agent Startup](#agent-startup)
    - [Connection Invitation Creation](#connection-invitation-creation)
    - [User input Processing](#user-input-processing)
    - [Send a Basic Message](#send-a-basic-message)
  - [Alice Controller](#alice-controller)
    - [Agent Startup](#agent-startup-1)
    - [Accept Invitation](#accept-invitation)
    - [User input Processing](#user-input-processing-1)
    - [Send a Basic Message](#send-a-basic-message-1)
- [**Takeaways**](#takeaways)


## **Overview**

In this lab, we spin up a couple of Aries agents, establish connections between them and have them exchange messages using the Aries `Basic Message` Protocol.


## **How to Run**

This lab from the ACA-Py repository includes details about running the example locally using Docker, on Play with Docker, and even has some guidance on running the lab without Docker. As always, we recommend running the lab using Docker, so you don’t get bogged down in technical issues unrelated to the lessons of the lab.


## **Instructions**

This tutorial in the ACA-Py repository spins up agents for Alice and Faber and has them connect and exchange messages. Follow the [instructions here](https://github.com/hyperledger/aries-cloudagent-python/tree/master/demo#the-alicefaber-python-demo), stopping at the end of the “Exchanging Messages” section. We’ll do the rest of the tutorial later (which admittedly, isn’t much!).

One important thing to understand about this particular demo is the agent and controller integration. As we stressed in the course, ACA-Py runs two processes: one for the agent and one for the controller. However, in this demo it appears that the two run in one controller process—and that can be a little confusing. In fact, they don’t run in the same process. The demo uses a Python feature such that the controller starts the ACA-Py instance as a sub-process. Use the links below to see the relevant code for that:



*   AliceAgent is an instance of demo agent - [code](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/alice.py#L219)
*   Demo agent starts a sub-process that is an instance of ACA-Py - [code](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/support/agent.py#L239)

There has been discussion of changing this demo to make the separation of controller and ACA-Py instance more obvious. In a later lab we’ll see examples of other controllers for Alice and Faber using the same ACA-Py instance, making the separation more obvious.


## **Navigating the Code**

Now let’s take a look at the controller code. We’ll cover here the important parts of the controllers starting up, connecting and sending text messages. In a later lab, we’ll complete the demo through issuing and proving verifiable credentials and cover those parts of the controller code. Since we aren’t dealing with verifiable credentials in this part of the code walkthrough, little of what is covered here relates to Indy or an Indy ledger.

Note that the links to specific lines in the code go to a specific version of the file in GitHub that may not be the latest. As such, the line numbers in GitHub may be slightly different than what is on your system (the latest version).



*   Alice agent code is in the repo file [demo/runners/alice.py](https://github.com/hyperledger/aries-cloudagent-python/blob/master/demo/runners/alice.py)
*   Faber agent code is in the file [demo/runners/faber.py](https://github.com/hyperledger/aries-cloudagent-python/blob/master/demo/runners/faber.py)
*   Both Alice and Faber are instances of [demo/runners/support/agent.py](https://github.com/hyperledger/aries-cloudagent-python/tree/master/demo/runners/support/agent.py)


### Faber Controller


#### Agent Startup



*   The [“main” function](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L117) to start the controller and agent.
    *   “genesis = await …” get the genesis file for the reading/writing to the ledger.
    *   “agent = FaberAgent …” start an agent instance.
        *   Call to the (parent) [controller class](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L31) to initialize the controller.
        *   Note the specific details about Faber (e.g. port numbers) and the extra ACA-Py startup parameters just for Faber.
    *   “await agent.listen_webhooks …” setup for receiving events from ACA-Py.
        *   Parent [method](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/support/agent.py#L307) that initializes webhooks and route handlers.
            *   Note below the functions for receiving and handling webhooks from ACA-Py. These functions are called when an event happens in ACA-Py that the controller needs to know about.
            *   Also just below that are the admin calls (request, GET and POST) for the controller to invoke the ACA-Py endpoints.
    *   “await agent.start_process … “ call to startup the ACA-Py instance process.
        *   Parent [method](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/support/agent.py#L269) that starts the ACA-Py instance sub-process.
            *   The ACA-Py process is separate from the controller process.
        *   “agent_args = …” prepare ACA-Py startup arguments.
            *   [Function](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/support/agent.py#L160) that gathers all the ACA-Py arguments to use, defaults, specific ports, URLs, wallet (storage info), optional demo arguments and controller-specific arguments. So many!!!
            *   Recall our earlier look at all of the possible ACA-Py startup arguments as you look at how many we are using in this example.
*   The [method in the agent class](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/support/agent.py#L75) to initialize the controller instance.
    *   Like ACA-Py, many parameters may be passed in to control specific behavior. As seen above, Faber only specifies a handful of those parameters.
    *   “self.ident = …“ defaulting of parameters as needed.
    *   “if RUN_MODE …” is special handling to support running on “[Play with Docker](https://labs.play-with-docker.com/)”.
    *   “self.storage_type = …” specify the type and details of the agent storage to be used.
        *   The demo supports (with appropriate configuration) the use of SQLite (default) or PostgreSQL Indy agent storage.
        *   Although still part of the indy-sdk, agent storage will soon be moved from Indy to Aries, as there is not an Indy (DID ledger, credential exchange) element to agent storage.


#### Connection Invitation Creation



*   [Generate](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L159) an invitation that Alice can use to connect.
    *   “connection = await …” call to ACA-Py to create an invitation.
    *   “await agent.detect_connection …” wait a response to the invitation.


#### User input Processing



*   [Main loop](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L175) for processing command line input from the user.


#### Send a Basic Message



*   The user [chose Option 3](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/faber.py#L246), send a message.
    *   Prompt for the message.
    *   “await agent.admin_POST …” invoke ACA-Py to start an instance of the Basic Message protocol ([RFC 0095](https://github.com/hyperledger/aries-rfcs/tree/master/features/0095-basic-message)).


### Alice Controller


#### Agent Startup

The startup of the Alice controller is almost the same as Faber, so we’ll leave the review of that part of the code as an exercise for the reader. Much of the differences between the two in the areas that relate to the handling of verifiable credentials, which we cover in a later exercise.


#### Accept Invitation



*   [Prompt for and receive the text invitation](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/alice.py#L167), as pasted in by the user.
    *   “try … url = …“ first try at parsing the invitation text.
        *   The controller allows flexibility in what the user pastes in. It could be a URL with a base64 invitation as a query parameter, only the base64 query parameter, or the already decoded JSON of the invitation.
        *   Or it might be an improperly constructed invitation and so not a valid invitation at all.
    *   “connection = await …” invoke the ACA-Py endpoint for processing a received invitation.
        *   Since the “--auto-accept-invites” ACA-Py startup parameter is used, the controller just has to wait for the ACA-Py instance to complete the connection handling here: “await agent.detect_connection …”


#### User input Processing



*   **[Main loop](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/alice.py#L232)** for processing command line input from the user.


#### Send a Basic Message



*   The user [chose Option 3](https://github.com/hyperledger/aries-cloudagent-python/blob/ab8097d199ae07a31459509eec007451483526e3/demo/runners/alice.py#L237), send a message.
    *   Prompt for the message.
    *   “await agent.admin_POST …” invoke ACA-Py to start an instance of the Basic Message protocol ([RFC 0095](https://github.com/hyperledger/aries-rfcs/tree/master/features/0095-basic-message)).

While we won’t go into detail here about the internals of ACA-Py (since developers that write controllers don’t need to do that), for the curious, here are the links to the ACA-Py code for the [connections](https://github.com/hyperledger/aries-cloudagent-python/tree/master/aries_cloudagent/protocols/connections) and [basic message](https://github.com/hyperledger/aries-cloudagent-python/tree/master/aries_cloudagent/protocols/basicmessage) protocol handlers.


## **Takeaways**

This lab demonstrates:



*   Starting agents.
*   Generating an invitation using the connection protocol ([RFC 0160](https://github.com/hyperledger/aries-rfcs/tree/master/features/0160-connection-protocol)).
*   Processing an invitation.
*   Sending a basic message using the basic message protocol ([RFC 0095](https://github.com/hyperledger/aries-rfcs/tree/master/features/0095-basic-message)).
*   Receiving a basic message.

This lab provides a good introduction to the construction of a controller for an ACA-Py instance. Developers should focus on connecting what they see on the command line with the code that is making that happen.

While the controllers here are quite simple, we’ve covered a lot of what makes an application a controller. Much of the additional complexity will not be in controller-specific capabilities but rather in the normal complexity of writing a business/web application.

That's it for this lab! Please return to the course.


<!-- Docs to Markdown version 1.0β18 -->
