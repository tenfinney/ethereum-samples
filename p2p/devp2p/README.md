# p2p programming in go-ethereum

These code examples are intended to demonstrate the main building blocks of peer-to-peer comunications in go-ethereum. They are organized in chapters, where every example in a chapter builds on the next.

They form the basis for a tutorial with a detailed simple-to-follow narrative. This tutorial is currently being written, and includes to date explanations of examples **A1** through **A4**. 

Please note that the texts are still in draft status, and may contain omissions, typos, shitty language and most certainly bad formatting. They is written in `latex`, but for convenience a README.md file will be generated with each update of the texts. It will be auto-generated by `pandoc` and may contain unparsed directives. It will stay that way until the document is complete, where proper builds will be made available.

## USING THESE EXAMPLES

```
go run <filename> [-v]
```

## TODO

* Write general introduction to components in go-ethereum devp2p
* Write accompanying tutorials
* Add example of lowlevel PSS implementation

## Contents

### A - Lowlevel devp2p

p2p server is the core structure for communications between nodes. It creates and maintains ip connections between nodes, and embeds p2p encryption with RLP serialization (RLPx) on the data connection.

* A1_Server.go 

  Initializing and starting the p2p Server

* A2_Connect.go

  Connecting two p2p Servers

* A3_Events.go

  Receiving notification of completed connection

* A4_Message.go

  Sending a message from server A to server B

* A5_Reply.go

  A sample p2p ping protocol implementation

### B - Remote Procedure Calls

* B1_RPC.go

  Create IPC RPC server with one method and call it  

* B2_Method.go

  Retrieve information from p2p server through RPC

* B3_Message.go

  Receive notification of p2p messaging events through RPC

### C - Service node

This entity encapsulates the p2p server and the RPC call APIs, in packages called "services." A Node.Service is defined as an interface, and objects of this interface are registered with the node, and automatically started in alphabetical order when the service node is started.

* C1_Stack.go

  Create and start a service node

* C2_Nodeinfo.go

  Local accessors to RPC APIs

* C3_Service.go

  Defining and running a service

* C4_Full.go

  Servicenode ping protocol implementation controlled through RPC

### D - Complex nodes

`devp2p` provides a framework for designing autonomous protocol handling code. This chapter shows how to implement one, and how to combine several services providing their own APIs and protocols in the same service node.

* D1_Protocols.go

  p2p protocol abstraction layer enabling automatic recognition of messages and external message handlers

* D2_Multiservice.go

  Registering multiple services with the service node

### E - Pss

Pss enables encrypted messaging between nodes that aren't directly connected through p2p server, by relaying the message through nodes between them. Relaying is done with swarm's kademlia routing. The message is encrypted end-to-end using ephemeral public key cryptography. 

* E1_Pss.go

  Set up a pss-activated swarm node, and send a message using public key encryption. 

* E2_PssRouting.go

  Demonstrates how to perform dark routing in pss.

* E3_PssSym.go

  Create an arbitrary symmetric encryption key, and send message with it.

* E4_PssRaw.go

  Send a message using external encryption

* E5_PssHandshake.go

  Using the builtin convenience method for Diffie-Hellmann key exchange.

* E6_PssProtocol.go - **broken**

  Implementing devp2p style protocols over pss.

* E7_PssClient.go - **broken**

  Mounting devp2p style protocols on an RPC connection.
