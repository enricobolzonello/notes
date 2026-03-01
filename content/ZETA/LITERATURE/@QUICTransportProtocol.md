---
connections: 
reference:
tags: 
 - type/paper
type: literature_note
created: 2025-12-21 15:40
modified:
citekey: QUICTransportProtocol
status: unread
dateread:
---

> [!Cite]
> [1] «The QUIC Transport Protocol | Proceedings of the Conference of the ACM Special Interest Group on Data Communication», ACM Conferences. Consultato: 20 dicembre 2025. [Online]. Disponibile su: [https://dl.acm.org/doi/10.1145/3098822.3098842](https://dl.acm.org/doi/10.1145/3098822.3098842)


>[!Synthesis]
>**Contribution**:: 
>
>**Strong Points**::
>
>**Weak Points**::
>
>**Related**:: 
>

>[!Metadata]
>    
> **Title**:: The QUIC Transport Protocol | Proceedings of the Conference of the ACM Special Interest Group on Data Communication  
> **Year**:: Error: `format` can only be applied to dates. Tried for format object   
> **Citekey**:: QUICTransportProtocol  
> **itemType**:: webpage    

> [!LINK] 
> > [QUICTransportProtocol.pdf](file:///Users/enricobolzonello/Zotero/storage/KNYU3XWF/QUICTransportProtocol.pdf).


> [!Abstract]
> We present our experience with QUIC, an encrypted, multiplexed, and low-latency transport protocol designed from the ground up to improve transport performance for HTTPS traffic and to enable rapid deployment and continued evolution of transport mechanisms. QUIC has been globally deployed at Google on thousands of servers and is used to serve traffic to a range of clients including a widely-used web browser (Chrome) and a popular mobile video streaming app (YouTube). We estimate that 7% of Internet traffic is now QUIC. We describe our motivations for developing a new transport, the principles that guided our design, the Internet-scale process that we used to perform iterative experiments on QUIC, performance improvements seen by our various services, and our experience deploying QUIC globally. We also share lessons about transport design and the Internet ecosystem that we learned from our deployment.


# Notes
- transport designed to replace HTTP/2, TLS and TCP
- Features
    - multiplexes multiple requests/responses over a single connection by providing each with its own stream, so that no response can be blocked by another
    - encrypts and authenticates packets
    - improves loss recovery by using unique packet numbers and by using explicit signaling in ACKs
    - allows connections to migrate across IP address changes by using a Connection ID to identify connections
    - provides flow control to limit the amount of data buffered at a slow receiver
    - ensures that a single stream does not consume all the receiver’s buffer
- servers should send header “Alt-Svc” in HTTP responses to say they support QUIC.


# Annotations%% begin annotations %%


%% end annotations %%

%% Import Date: 2025-12-21T15:40:28.030+01:00 %%
