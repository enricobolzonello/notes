---
connections:
reference: "[[Modello OSI]]"
tags:
type: literature_note
created: 2025-12-21 16:07
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

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

## Service Access Point (SAP)
The SAP is a conceptual location at which one OSI layer can request the services of another layer of the stack.

example: PD-SAP or PLME-SAP. The Medium Access Control (MAC) layer requests certain services from the physical layer

---

# Questions
#flashcards/stem  

What is the OSI Model?::7-layer model that describes communications from the physical implementation of transmitting bits to the highest level representation of data
<!--SR:!2026-02-27,1,230-->

What is a Service Access Point (SAP) in networking?::location where one OSI layer can communicate with another layer
<!--SR:!2026-02-27,1,230-->