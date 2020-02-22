<!----- Conversion time: 0.651 seconds.


Using this Markdown file:

1. Cut and paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β18
* Sat Feb 22 2020 09:42:58 GMT-0800 (PST)
* Source doc: https://docs.google.com/a/cloudcompass.ca/open?id=1m6ZSXkJ_rZq-S3mdsiVRDmKRP-8Ek3XJgLDrh10I0-U
----->



# **Lab: Executing a Protocol**


## **Overview**

In this lab, we’ll go back to you being the controller. We'll use an OpenAPI/Swagger user interface to allow you to be an Aries agent controller. As well, we’ll use a couple of demo options to ensure you are executing each step of the protocols, and that you are seeing the webhook data that comes back from ACA-Py. In this way, you will be seeing and preparing the data exactly as would a controller.


## **How to Run**

This lab from the ACA-Py repository includes details about running locally using Docker, and on Play with Docker. As always, we recommend running the lab using Docker, so you don’t get bogged down in technical issues unrelated to the lessons of the lab.


## **Instructions**

To prepare to run the lab, clone the ACA-Py github repo (locally or on Play with Docker):


```
git clone https://github.com/hyperledger/aries-cloudagent-python
cd aries-cloudagent-python
```


Go to the [instructions here](https://github.com/hyperledger/aries-cloudagent-python/blob/master/demo/AriesOpenAPIDemo.md) in the ACA-Py repository. As you carry out the instructions, keep track of who you are on each step (Alice’s or Faber’s controller) and how you would code an application to automate the manual steps in a generalized way. For example:



*   If you really were Faber’s controller, how would you handle executing thousands of protocol instances running in parallel between you and all of Faber’s alumni?
*   How would you interface with Faber College’s backend information systems?
*   How would you structure Alice’s controller if her Aries agent was running on her phone?


## **Takeaways**

This lab demonstrates executing the HTTP interfaces used by instances of ACA-Py and their controllers (in this case, you) to execute Aries protocols. It shows: 



*   Controllers initiating several protocols:
    *   Alice initiating a connection protocol ([RFC 0160](https://github.com/hyperledger/aries-rfcs/tree/master/features/0160-connection-protocol)).
        *   Although Faber did take the first step, Alice initiated the interaction protocol by accepting the invitation.
    *   Alice initiating a basic message protocol ([RFC 0095](https://github.com/hyperledger/aries-rfcs/tree/master/features/0095-basic-message)).
    *   Faber initiating an issue credential protocol ([RFC 0036](https://github.com/hyperledger/aries-rfcs/tree/master/features/0036-issue-credential)).
    *   Faber initiating a present proof protocol ([RFC 0037](https://github.com/hyperledger/aries-rfcs/tree/master/features/0037-present-proof)).
*   Events from ACA-Py being received by controllers via a webhooks as the protocol moves forward.
*   The controller pulling data from the events to process and respond to those events.

This lab provides a good introduction to the inner workings of controllers as they step through Aries protocols. It also makes it easy to see the interactions between the controller, the agent framework (ACA-Py in this case) and other agents.

That's it for this lab! Please return to the course.


<!-- Docs to Markdown version 1.0β18 -->
