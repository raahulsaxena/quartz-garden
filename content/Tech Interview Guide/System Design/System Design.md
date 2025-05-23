---
title: High Level System Design
tags:
- system design
- interview prep
- architecture
- scalability
created: 2024-06-09
updated: 2024-06-09
---


### Resources
---
- [Awesome SD Resources](https://github.com/ashishps1/awesome-system-design-resources)
- [System Design Primer](https://github.com/donnemartin/system-design-primer)
- [NeetCode - System Design Course](https://neetcode.io/courses/system-design-interview/0)
- [DailyCodeBuffer](https://www.youtube.com/@DailyCodeBuffer)
- Blogs
	- [Engineering at Meta](https://engineering.fb.com/)
	- [The Netflix Tech Blog](https://netflixtechblog.com/)
	- [LinkedIn Engineering: Blog](https://www.linkedin.com/blog/engineering)
	- [Instagram Engineering](https://engineering.fb.com/tag/instagram/)
	- [Old Instagram Blog](https://instagram-engineering.com/)
	- [Pinterest Engineering](https://medium.com/pinterest-engineering)
	- [Dropbox Engineering Blog](https://dropbox.tech/)
	- [Etsy Engineering](https://www.etsy.com/codeascraft)
	- [Booking.com Tech Blog ](https://blog.booking.com/)
	- [The Airbnb Tech Blog](https://medium.com/airbnb-engineering)
	- [Stripe Engineering Blog](https://stripe.com/blog/engineering)
- Guides
	- [System Design Interview - interviewing.io](https://interviewing.io/guides/system-design-interview)
	- HelloInterview website
- Books
	- [[grokking-the-system-design-interview.pdf]]
	- [[Designing_Data-Intensive_Applications_TH.pdf]]
	- [[Database Internals.pdf]]
- Videos
	- Jordan has no life
	- System Design Fight Club YouTube
	- System Design Interview YouTube Channel
	- ByteByteGo


## System Design Interview

[https://www.tryexponent.com/blog/system-design-interview-guide](https://www.tryexponent.com/blog/system-design-interview-guide)

The system design interview assesses your ability to tackle complex engineering problems by designing a system or component from scratch.

For example,

- Design TikTok.
- Design WhatsApp.
- How would you optimize CDN usage for Netflix?

Instead, you'll be judged on your ability to:

- Understand and dissect technical problems,
- Sketch blueprints,
- Engage in discussions about system requirements and tradeoffs,
- Create working solutions.

Interviewers don’t expect you to create a 100% perfect solution.

Instead, system design interviews evaluate how you make decisions in the face of uncertainty, your confidence in taking risks, and your ability to adapt to changing technical requirements.


➤ 𝗦𝘆𝘀𝘁𝗲𝗺 𝗗𝗲𝘀𝗶𝗴𝗻 𝗣𝗿𝗼𝗷𝗲𝗰𝘁𝘀:  
  
1. Content Delivery Network  
- [https://lnkd.in/deNyycnF](https://lnkd.in/deNyycnF)  
- Edge computing, caching strategies, load balancing, and fault-tolerance.  
  
1. Distributed Chat Application  
- [https://lnkd.in/dh-KhC7Q](https://lnkd.in/dh-KhC7Q)  
- Web Sockets, real-time communication, event-driven architecture, and distributed systems.  
  
1. Online Marketplace  
- [https://lnkd.in/dGHBHwiT](https://lnkd.in/dGHBHwiT)  
- User authentication, catalog management, payment integration, and fault-tolerant architecture.  
  
1. Ride-sharing Service  
- [https://lnkd.in/ddU_jYtC](https://lnkd.in/ddU_jYtC)  
- Geolocation services, distributed databases, real-time matching algorithms, and microservices.  
  
1. Scalable URL Shortener  
- [https://lnkd.in/ddrNJRcZ](https://lnkd.in/ddrNJRcZ)  
- URL hashing, database sharding, load balancing, and horizontal scaling.  
  
➤ 𝗠𝗶𝗰𝗿𝗼𝘀𝗲𝗿𝘃𝗶𝗰𝗲𝘀 𝗣𝗿𝗼𝗷𝗲𝗰𝘁𝘀:  
  
1. Event-Driven Order Processing  
- [https://lnkd.in/d52MTcz9](https://lnkd.in/d52MTcz9)  
- Event streaming with Kafka, CQRS pattern, and message-driven microservices.  
  
1. Hotel Booking System  
- [https://lnkd.in/d4JvrcdB](https://lnkd.in/d4JvrcdB)  
- Event-driven architecture, payment gateway integration, and distributed data consistency.  
  
1. E-commerce Microservices  
- [https://lnkd.in/dZNxYU6p](https://lnkd.in/dZNxYU6p)  
- [https://lnkd.in/d-ZEvtwR](https://lnkd.in/d-ZEvtwR)  
- Modular architecture, RESTful APIs, database integration, and containerization with Docker/Kubernetes.  
  
1. Inventory Management System  
- [https://lnkd.in/dUbRHVkA](https://lnkd.in/dUbRHVkA)  
- Microservice communication (gRPC/REST), database transactions, and real-time inventory updates.  
  
1. Blogging Platform  
- [https://lnkd.in/dxdJVJST](https://lnkd.in/dxdJVJST)  
- Scalable content management, authentication, authorization, and multi-service communication.  
  
These projects give a solid foundation to showcase your abilities in System Design, DSA, and Microservices in interviews. If possible, try implementing one or two projects yourself, adding your personal touch to stand out even more!  
  
Hope these ideas help you level up for your next interview.  
  
𝗜 𝗵𝗮𝘃𝗲 𝗽𝗿𝗲𝗽𝗮𝗿𝗲𝗱 𝗶𝗻 𝗗𝗲𝗽𝘁𝗵 𝗦𝘆𝘀𝘁𝗲𝗺 𝗗𝗲𝘀𝗶𝗴𝗻 𝗚𝘂𝗶𝗱𝗲

𝗦𝗰𝗮𝗹𝗮𝗯𝗹𝗲 𝗦𝘆𝘀𝘁𝗲𝗺 𝗗𝗲𝘀𝗶𝗴𝗻:  
1. Design a URL shortening service like Bitly.  
2. Design a scalable social media feed system (e.g., Facebook News Feed)?  
3. Design an online book reader system (similar to Kindle).  
4. Design a global ride-sharing service like Uber?  
5. Design a video streaming platform like YouTube or Netflix.  
6. Design a scalable chat application like WhatsApp or Slack?  
7. Design an e-commerce search system for a platform like Flipkart or Amazon.  
8. Design a file storage and sharing service like Google Drive or Dropbox?  
9. Design a real-time collaborative document editor like Google Docs.  
10. Design a scalable notification system (e.g., push notifications for a mobile app)?  
  
𝗥𝗲𝗮𝗹-𝘁𝗶𝗺𝗲 𝗦𝘆𝘀𝘁𝗲𝗺𝘀 & 𝗔𝗻𝗮𝗹𝘆𝘁𝗶𝗰𝘀:  
11. Design a rate limiter for an API.  
12. Design a system to detect fraudulent transactions in real-time?  
13. Design a system for tracking and monitoring the location of delivery packages.  
14. Design a real-time analytics dashboard (e.g., for monitoring website traffic)?  
15. Design a live auction/bidding platform (e.g., eBay auctions).  
16. Design a distributed cache system like Redis or Memcached?  
17. Design a scalable logging and monitoring system (e.g., similar to ELK Stack).  
18. Design a leaderboard system for an online game?  
  
𝗦𝗲𝗮𝗿𝗰𝗵 & 𝗥𝗲𝗰𝗼𝗺𝗺𝗲𝗻𝗱𝗮𝘁𝗶𝗼𝗻 𝗦𝘆𝘀𝘁𝗲𝗺𝘀  
9. Design a search autocomplete feature (e.g., Google Search suggestions).  
10. Design a recommendation system for an e-commerce platform?  
11. Design a system for ranking search results (e.g., Google Search PageRank).  
12. Design a product recommendation system similar to Amazon's "Customers who bought this also bought"?  
  
𝗛𝗶𝗴𝗵 𝗧𝗿𝗮𝗳𝗳𝗶𝗰 & 𝗖𝗼𝗻𝘁𝗲𝗻𝘁 𝗗𝗲𝗹𝗶𝘃𝗲𝗿𝘆  
5. Design a content delivery network (CDN) like Cloudflare or Akamai.  
6. Design a distributed ad-serving system (e.g., Google Ads)?  
7. Design a scalable event ticketing platform (e.g., Ticketmaster).


Topics:

**System Design Topics Covered:** 

1. Introduction to System Design 
2. Scalability and Performance 
3. Latency and Throughput 
4. Architectural Patterns 
5. Availability and Availability Patterns 
6. Replication 
7. Consistency and Consistency Patterns 
8. CAP Theorem 
9. PACELC Theorem 
10. Database and Storage 
11. Relational Databases 
12. Database Isolation Levels 
13. Scaling Databases 
14. Sharding and Partitioning 
15. Non-Relational Databases 
16. Choosing the Right Database 
17. Caching 
18. Asynchronous Processing 
19. Message Queues (Kafka, RabbitMQ) 
20. Monolithic vs. Microservices Architecture 
21. Event-Driven Architecture 
22. API Gateway and Backend for Frontend (BFF) 
23. REST, GraphQL, and gRPC 
24. Long Polling, WebSockets, Server-Sent Events (SSE) 
25. Design Patterns 
26. Resiliency 
27. Designing for Resiliency 
28. Load Balancers 
29. Circuit Breakers 
30. System Essentials 
31. Consistent Hashing 
32. Networking and Communication 
33. Real-World Architectures & Engineering Blogs