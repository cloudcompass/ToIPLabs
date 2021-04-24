# AgentBook - ACA-Py Alice Agent Lab Instructions

This demo shows how pairwise DIDs are used to establish a secure, end-to-end messaging
connection between two Aries Agents. The demo is part of the Linux Foundation 
course LFS172x, *[Introduction to Hyperledger Sovereign Identity Blockchain Solutions: Indy, Aries and Ursa](https://www.edx.org/course/introduction-to-hyperledger-sovereign-identity-blockchain-solutions-indy-aries-and-ursa)* that
available on edX.

Pairwise DIDs are the foundation of the DIDComm
protocol for sending messages between agents. As discussed in the course, the 
DIDComm envelope protocol is used to send messages between agents, and any number of
content protocols are sent within those envelopes to do...almost anything. For
example, in this demo we will use several content protocols, including `Connection` to 
establish a connection between two agents, `Trust Ping` to confirm the
connection is functional, and `Basic Message` to send a text message from one agent
to the other. The [Aries RFCs repo](https://github.com/hyperledger/aries-rfcs/) contains
a list of connection protocols that have been proposed, implemented and, in some cases,
accepted by the Aries Working Group.

For this demo we'll use [Play with Docker](https://labs.play-with-docker.com) a tool from Docker, Inc. that allows you to access a Linux command line and run docker scripts in your browser. We'll also use AgentBook, a test service for Aries agents run by the Government of British Columbia's [VON Team](https://vonx.io).

## Demo Steps

- Go to [https://labs.play-with-docker.com](https://labs.play-with-docker.com) (called Play with Docker)
- Click `Start` and the `+ Add New Instance` to start a terminal window
- In the terminal window, copy, paste and execute the following commands:

```
git clone https://github.com/hyperledger/aries-cloudagent-python
cd aries-cloudagent-python/demo/
LEDGER_URL=http://dev.bcovrin.vonx.io ./run_demo alice
```

- In a separate browser tab go to AgentBook, at URL [http://agentbook.vonx.io](http://agentbook.vonx.io)
- Click `Generate Invitation`
- Click `Copy Invitation` (or select and copy)
- Return to your Play With Docker tab. You should be at a prompt to `Enter your Invitation`.
  - If your agent is still initializing, wait for it to complete.
- At the prompt, paste in the invitation copied from AgentBook (Right Click, select Paste)
  - a connection should be established and you have some options on what you can do
- Type "3" and type a message to AgentBook (e.g "Hello AgentBook")
- See the response "AgentBook has received your message"
- Switch browser tabs to AgentBook
- Click `Go to Connection`
- You should see the sequence of messages exchanged between the agents, including the text message.
  - The messages are in reverse chronological order (bottow up) and are grouped by the protocols executed:
    - Invitation and DID exchange
    - Trust Ping from Alice and response from AgentBook
    - Message from Alice 
    - Auto-reply message from AgentBook
- Use the `Send Message` area to send a message to Alice
- Return to Play with Docker and verify that the message was received.
- Type `X` to end the Alice session.
- Close up the browsers.

That's it!

In that demo you saw two agents establishing a connection and then using the `Trust Ping` and `Basic Message` protocols to verify the connection was working correctly. Every message sent was end-to-end encrypted for the recipient using the key material provided in the pairwise DID provided by the recipient during the DID-Exchange process.

Source code to review:

- Aries Cloud Agent - Python and the Alice agent: [https://github.com/hyperledger/aries-cloudagent-python](https://github.com/hyperledger/aries-cloudagent-python) - `/demo` folder.