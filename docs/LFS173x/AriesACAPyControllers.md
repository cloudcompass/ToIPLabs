<!----- Conversion time: 0.723 seconds.


Using this Markdown file:

1. Cut and paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β18
* Sat Feb 22 2020 08:52:25 GMT-0800 (PST)
* Source doc: https://docs.google.com/a/cloudcompass.ca/open?id=1QRXAA4W6U1QP2Q4t7IvfBMpfIGD-8khsswS88-WmerM
----->



# Lab: Python Not For You?

## **Overview**

In this lab, we'll go through three examples of Web controllers for ACA-Py using three different tech stacks. The story will be the same--Alice, Faber and ACME--but this time instead of running on the command line, the agent UI will be in browser tabs. Instead of Python, the code is in Angular, .Net and NodeJS/Express. Enjoy the variety!

## **How to Run**

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:

- [Running LFS173x Labs](RunningLabs.md)

## **Instructions**

This lab does not use the ACA-Py repo, but instead references it. The lab uses docker-compose to start everything up, including the same Alice, Faber and Acme agents used in the earlier labs. To prepare to run the lab, clone the ACA-Py github repo (locally or on Play with Docker):

```
git clone https://github.com/petridishdev/aries-acapy-controllers
cd aries-acapy-controllers/AliceAcmeFaberDemo
```

The instructions for getting started with the coding [are here](https://github.com/petridishdev/aries-acapy-controllers/tree/master/AliceFaberAcmeDemo). The instructions include a section called “Running Locally” about running on a local machine without Docker. As always, we recommend not doing that the first time through, so you get the benefit of the demo without battling through getting everything installed and working on your specific machine configuration.

## The Code

If you missed the link to look through the code, we recommend that you go back to the link (here). That document will give you a flavour for the controller functionality as implemented in different tech stacks.

## **Takeaways**

Same old story, same old ACA-Py, brand new controllers. With this demo, we get away from Python development, still perform the same actions, but in other tech stacks. And, we (finally!) get away from the command line and provide a browser-based interface.

As we’ve mentioned (too often, we’re sure), the biggest thing you should notice is that controller development is very much like web development:

* Loop:
  *   Wait for an event
  *   Determine what to do about the event
  *   Optionally—send a request in response to the event

That's it for this lab! Please return to the course.

<!-- Docs to Markdown version 1.0β18 -->
