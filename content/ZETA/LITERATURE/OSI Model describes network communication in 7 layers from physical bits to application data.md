---
up:
tags:
  - atomic
created: 2025-12-21 16:07
---
> Model that describes communications from the physical implementation of transmitting bits across a transmission medium to the highest level representation of data of a distributed application

It is a 7-layer architecture used to define how data moves across a network.

In practice it is not implemented (TCP/IP is), but it is a standard reference.

![[OSI Model.png]]

| Layer | Name         | Protocol Data Unit (PDU) | Function                                                                                                                                         |
| ----- | ------------ | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| 7     | Application  | Data                     | High-level protocols such as for resource sharing or remote file access, e.g. HTTP                                                               |
| 6     | Presentation | Data                     | Translation of data between a networking service and an application; including character encoding, data compression and encryption/decryption    |
| 5     | Session      | Data                     | Managing communication sessions, i.e., continuous exchange of information in the form of multiple back-and-forth transmissions between two nodes |
| 4     | Transport    | Segment                  | Reliable transmission of data segments between points on a network, including segmentation, acknowledgement and multiplexing                     |
| 3     | Network      | Packet, Datagram         | Structuring and managing a multi-node network, including addressing, routing and traffic control                                                 |
| 2     | Data link    | Frame                    | Transmission of data frames between two nodes connected by a physical layer                                                                      |
| 1     | Physical     | Bit, Symbol              | Transmission and reception of raw bit streams over a physical medium                                                                             |
|       |              |                          |                                                                                                                                                  |

# See also 
- [[An IP Address Identifies the Location of a Resource Within a Network]] — IP operates at Layer 3 (Network); the OSI model is the framework that gives IP addressing its place in the stack 
- [[A process in operating systems is a program in execution]] — processes communicate across the network through the Application layer (7) down to the Physical layer (1); the OSI model is the bridge between OS processes and the network 
- [[@QUICTransportProtocol]] — QUIC operates at Layer 4 (Transport), replacing TCP; understanding its position in the OSI stack explains what guarantees it provides 
# References 
- [[Modello OSI]]


---

# Questions
#flashcards/stem  

What is the OSI Model?::7-layer model that describes communications from the physical implementation of transmitting bits to the highest level representation of data
<!--SR:!2026-02-27,1,230-->