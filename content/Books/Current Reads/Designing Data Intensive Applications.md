---
title: Designing Data Intensive Applications
created: 2025-07-06
tags:
    - book-notes
    - technical-books
    - ddia
    - system-design
---

### Chapter 1: Reliable, Scalable and Maintainable Applications.

Many applications need to
- Store data so that they or another application can find it again later (Databases)
- Remember the result of an expensive operation, to speed up reads (caches)
- Allow users to search data by keyword or filter it in various ways (search indexes)
- Send a message to another process, to be handled asynchronously (stream processing)
- Periodically crunch a large amount of accumulated data (batch processing)

Many new tools for data storage and processing have emerged in recent years. They are optimized for a variety of different use cases and no longer neatly fit into traditional categories. For example: there are datastores that are also used as message queues (Redis) and there are message queues with database-like durability guarantees (Apache Kafka).

![[DDIA-1-1.png]]


There are 3 concerns that are important in most software systems:

- **Reliability**: System should continue to work *correctly* (performing the correct function at the desired level of performance) even in the face of adversity (hardware or software faults and even human error)
- **Scalability**: As the system grows (in data volume, traffic volume or complexity), there should be reasonable ways of dealing with that growth.
- **Maintainability**: Over time, many different people will work on the system, and they should all be able to work on it *productively*.

#### Reliability

Typical expectations from something that is reliable include:
- The application performs the function that the user expected.
- It can tolerate the user making mistakes or using the software in unexpected ways.
- Its performance is good enough for the required use case, under the expected load and data volume.
- The system prevents unauthorized access and abuse.

Reliability roughly means - continuing to work correctly even when things go wrong.

The things that can go wrong are called faults and systems that anticipate faults and can cope with them are called fault tolerant or resilient.

Fault is not the same as failure.

A fault is usually defined as one component of the system deviating from its spec whereas a failure is when the system as a whole stops providing the required service to the user.

We want to design fault-tolerance mechanisms that prevent faults from causing failures.

**Read about Netflix Chaos Monkey.**

#### Software Errors

We usually think of hardware faults as being random and independent from each other.

Another class of fault is a systematic error within the system. Like A software bug that causes every instance of an application server to crash when given a particular bad input. Sometimes, these include cascading failures, where a small fault in one component triggers a fault in another component, which in turn triggers further faults.

#### How important is reliability?

It is not just for nuclear power stations and air traffic control software - more mundane applications are also expected to work reliably. 

Bugs in business applications cause lost productivity and outages of ecommerce sites can have huge costs in terms of lost revenue and damage to reputation.

#### Scalability

It is the term used to describe a system's ability to cope with increased load. 
But it is not a one-dimensional label.

Even if a system is working reliably today, that doesn't mean it will necessarily work reliably in the future. One reason for degradation is increased load - more concurrent users or larger volumes of data being processed.

Page 11


Page 27 onwards

# Chapter 2: Data Models and Query Languages


Most applications are built by layering one data model on top of another. For each layer, the key question is: how it is *represented* in terms of the next lower layer.

- As an application developer, you look at the real world and model it in terms of objects and data structures, and APIs that manipulate those data structures.
- When you want to store those data structures, you express them in terms of a general purpose data model, such as JSON, XML documents, tables in a relational database, or a graph model.

Basic idea remains same - each layer hides the complexity of layers below it by providing a clean data model.

Since the data model has such a profound effect on what the software above it can and can't do, it's important to choose one that is appropriate to the application.

## Relational vs Document Model

The best known data model today is probably that of SQL. Data is organized into relations (called tables in SQL), where each relation is an unordered collection of tuples. (rows in SQL).

## Birth of NoSQL

Not only SQL.

Driving forces behind the adoption of NoSQL databases:
- A need for greater scalability than relational databases can easily achieve, including very large datasets or very high write throughput.
- A widespread preference for free and open source software over commercial database products.
- Specialized query operations that are not well supported by relational model
- Frustration with the restrictiveness of relational schemas, and a desire for a more dynamic and expressive data model.

## Object-Relational mismatch

Most application development today is done in object-oriented programming languages, which leads to a common criticism of SQL data model: 
- If data is stored in relational tables, an awkward translation layer is required between the objects in the application code and the database model of tables, rows, and columns.

Object relational mapping (ORM) frameworks like Hibernate reduce the amount of boilerplate required for this translation layer, but they can't completely hide the differences between the two models.

Some developers feel that the JSON model (document based model) reduces the impedance mismatch between the application code, and storage layer. 

Page 33