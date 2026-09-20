---
tags:
  - literature
up:
created: 2024-12-17 18:12
---

![cover|150](http://books.google.com/books/content?id=p1heDgAAQBAJ&printsec=frontcover&img=1&zoom=1&edge=curl&source=gbs_api)

# Designing Data-Intensive Applications

by [[Martin Kleppmann]]

## Summary
Data is at the center of many challenges in system design today. Difficult issues need to be figured out, such as scalability, consistency, reliability, efficiency, and maintainability. In addition, we have an overwhelming variety of tools, including relational databases, NoSQL datastores, stream or batch processors, and message brokers. What are the right choices for your application? How do you make sense of all these buzzwords? In this practical and comprehensive guide, author Martin Kleppmann helps you navigate this diverse landscape by examining the pros and cons of various technologies for processing and storing data. Software keeps changing, but the fundamental principles remain the same. With this book, software engineers and architects will learn how to apply those ideas in practice, and how to make full use of data in modern applications. Peer under the hood of the systems you already use, and learn how to use and operate them more effectively Make informed decisions by identifying the strengths and weaknesses of different tools Navigate the trade-offs around consistency, scalability, fault tolerance, and complexity Understand the distributed systems research upon which modern databases are built Peek behind the scenes of major online services, and learn from their architectures

## Table of Contents
- Basics
	- [[Reliability means preventing faults from causing failures]]
	- [[Scalability is a system's ability to cope with increased load|Scalability is a system's ability to cope with increased load]]
	- [[Most of the cost of software is maintenance (operability, simplicity, evolvability)]]
- Data Models and Query languages
	- each layer hides the complexity of the layers below it by providing a clean data model
	- [[Query Languages for Data]]
- Storage and Retrieval
	- there is a big difference between storage engines that are optimized for *transactional* workloads (OLTP) and those optimized for *analytics* (OLAP)
	- index: speed up queries, but slows down writes
		- [[An SSTable is a segment of key-value pairs sorted by keys]]
		- [[LSM-Trees]]

## Notes
- 


## Quotes
- 