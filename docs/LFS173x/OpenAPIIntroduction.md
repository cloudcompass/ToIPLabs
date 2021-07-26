# Lab: Using ACA-Py’s OpenAPI/Swagger Interface<!-- omit in toc -->

- [Overview](#overview)
- [How to Run](#how-to-run)
- [Instructions](#instructions)
  - [Using the OpenAPI Interface](#using-the-openapi-interface)
  - [The Usage Pattern](#the-usage-pattern)
- [Try It Out](#try-it-out)
  - [Explore](#explore)
  - [End the Lab](#end-the-lab)
- [Takeaways](#takeaways)

## Overview

In this lab, we'll introduce the ACA-Py OpenAPI/Swagger user interface.

## How to Run

This lab can be run locally with Docker or on Play with Docker in your browser. For general instructions for each, see the following:

- [Running LFS173x Labs](RunningLabs.md)

## Instructions

To prepare to run the lab, clone the ACA-Py github repo (locally or on Play with Docker):

```bash
git clone https://github.com/hyperledger/aries-cloudagent-python
cd aries-cloudagent-python/demo
LEDGER_URL=http://dev.greenlight.bcovrin.vonx.io ./run_demo faber

```

An instance of the Faber agent will start, initialize, generate and print an invitation. We’ve seen that before. For this case, we’re going to ignore the command line and open up port 8021 in a browser using the "8021" link in the header if you are on Play with Docker, or [http://localhost:8021/](http://localhost:8021/) if you are running locally. Either option should open a web page labelled "Faber Agent" with a long list of HTTP actions (GETs and POSTs). This is the OpenAPI/Swagger interface for the Faber ACA-Py instance that you started. Let’s explore what we can do.

### Using the OpenAPI Interface

The ACA-Py endpoints are in labelled groups ("server", "action-menu", "present-proof", and so on), each with member endpoints (e.g. "/plugins" , "/status", "/status/reset" and "/features" in the server group). Each of the endpoints are HTTP requests that your controller can make to an ACA-Py instance. This interface can be used as you develop your controller to experiment with each of the endpoints.

Click on an endpoint to try it out, such as the "/plugins" endpoint in the "server" group.

- You will see two sections, the parameters (none in this case) with a "Try it out" button, and a Responses section, initially with an example of what to expect back.
- Click the "Try it Out" button. The parameters section expands to provide inputs for the parameters, and a big "Execute."
- Since this example has no parameters, just click "Execute."
- The Responses section will expand to show:
  - The equivalent curl command.
  - The equivalent request URL.
  - The results (response code and body) from executing the HTTP request.
- In this case, the list of capabilities and protocols supported by the Faber ACA-Py instance.
- Click again on the endpoint header (e.g. "GET /plugins") to collapse the details for that endpoint.

To see an example of an endpoint with parameters, use the "connection" group and "GET /connections" endpoint. It presents a number of options for searching for connections. Try executing it once with no parameters to get all the connections currently active. There is just one right now—the one associated with the generated invitation that was printed to the log for Alice to use. To try the parameters, copy the value of the "state" field in the result ("invitation"), paste it in the "state" parameter input field and click "Execute" again. Unsurprisingly, you will see the same result.

Note that as the number of Aries protocols has increased, especially those that are part of Aries Interop Profiles (AIP) 1.0 and 2.0, and the number of supported protocols in ACA-Py has also increased. Accordingly, be careful when using the OpenAPI endpoints that you
are using the right **version** of the (for example) "present-proof" and "issue-credentials" protocol endpoints, as multiple versions may be supported.

### The Usage Pattern

Armed with the basics, we can define the basic pattern for using the tool:

1. Find the endpoint of interest.
2. Click on the endpoint name to expand its section of the UI.
3. Click on the "Try it out" button.
4. Fill in any data necessary to run the command.
5. Click Execute.
6. Check the response to see if the request worked and what was returned.

The mechanical steps are easy. It's the fourth step from the list above that can get tricky. Supplying the right data and, where JSON is involved (for a POST), getting the syntax correct—braces and quotes can be a pain. When the steps don’t work, start your debugging by looking at your JSON. Frequently, the parameters are IDs, and you can get those by copying and pasting the corresponding IDs from message results.

## Try It Out

Here is a sequence of steps you can follow. The guidance will be minimal—use the pattern above to fill in the six substeps of each task. Each endpoint we’ll use is in the "connections" group.

- Get a list of connections using the endpoint "/connections".
  - No parameters; result should be just one entry, the one started by the Faber controller as it spun up.
- Generate a new invitation using the endpoint "POST /connections/create-invitation".
  - Edit the `body`, as follows:
    - Remove the `mediation_id`, item and value.
    - Change the `my_label` value from "Bob" to something else, such as "Faber Agent."
    - Change the `routing_keys` value, to be an empty array (`[]`).
  - Edit the `Alias` to put in a value, such as your name.
  - Click the "Execute" button.
  - Result should look like a familiar invitation.
    - If you get an error, look at the body data and adjust as needed.
  - Copy the value of the `invitation` item in the result, from "{" to "}" (careful!!).
- Accept the invitation using the endpoint "POST /connections/receive-invitation".
  - In the `body` parameter, remove what's there and paste the copied invitation data from the previous step.
  - Result should be `200` status and a connection object with a "state" set to "request."
    - Didn’t work? Check your copying and pasting…
- Get a new list of connections using the endpoint "/connections".
  - No parameters, result should be three entries, with one in the `request` state, and the other two `invitations`
    - Why three? The original invitation, the invitation you created, and the one created from accepting the invitation.
  - Highlight and copy the value of the connection ID from the active connection.
- Get the specific active connection using the endpoint "/connections/{id}".
  - Parameter is the copied ID from the previous step in the "id" field (no double quotes).
  - Result should be the details of the one active connection.

What did we do? We just created a new invitation and used it to initiate a connection from Faber to itself. Nice!

### Explore

That’s it for the formal part of the lab, but we recommend that you spend a little time exploring the process. For example, you might want to
redo the "create invitation" steps you did above, but on both the create and accept, set the "auto-accept" parameter to true, to see
the state of the connections when that is done.

We have another lab using this API to perform the full Alice/Faber credential exchange.

### End the Lab

To complete the lab, return to the terminal used to start the Faber agent and click Ctrl-C to terminate it.

## Takeaways

The OpenAPI/Swagger interface is a great way to learn about the API that ACA-Py exposes to an agent. Rather than trying to understand the API by reading it, you can experiment with it and try out the endpoints that you are using. You should know the basics of how to use the interface and have a good idea of the core endpoints in a typical ACA-Py agent.

It’s a really good idea to get used to using this interface as it is a useful tool for trying things out. For example, suppose you are trying to experiment with a new Indy presentation request. It’s much faster to try to assemble the request through repeated tests in this interface versus a typical edit, deploy, test development loop.

An important thing to note about the API is that it is dynamic to the agent to which you are connected. For example, if extra protocols are added via the "`--plugin`" in the ACA-Py startup parameters, the endpoints for those protocols will appear on this page when connecting to that ACA-Py instance.

That's it for this lab! Please return to the course.
