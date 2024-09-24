+++
title = "api protocol landscape"

date = 2023-12-07
description = "REST still dominant, but..."
authors = []
draft = false

[taxonomies]
tags=[ "APIs" ]
+++


I really liked this post: ["The evolving landscape of API protocols in 2023"][post], by Alex Xu -- the content, the organization, and the graphics.

### nice ChatGPT summary

The article _"The Evolving Landscape of API Protocols in 2023"_ from the Postman blog, written by guest author Alex Xu, explores the current trends and developments in API protocols based on a survey of over 40,000 developers. It highlights the most popular API protocols and their advantages and limitations, providing insights into their growing or declining adoption rates.

__REST (Representational State Transfer)__ remains the most popular API architectural style, though its usage has slightly declined. Its simplicity, scalability, and platform-agnostic nature are key strengths, but challenges like over-fetching, chatty interfaces, and lack of real-time capabilities persist.

__Webhooks__, with a 36% adoption rate, are praised for enabling real-time event-driven communication without resource-heavy polling, but they require robust error handling and security measures.

__GraphQL__, used by 29% of developers, offers a flexible and efficient alternative to REST, allowing more precise data retrieval through single queries. However, its flexibility can introduce performance and security issues, and it has a steeper learning curve.

__SOAP__, though declining, remains relevant in industries requiring strict standards, security, and ACID-compliant transactions. Despite its complexity, it remains a dependable choice for specific use cases.

__WebSocket__ (25% usage) supports low-latency, bidirectional communication, making it suitable for real-time applications like chat systems. gRPC, a modern protocol by Google, is gaining traction due to its high performance, strong typing, and streaming support.

The article concludes that while REST remains foundational, the increasing complexity of modern applications calls for a more diverse toolkit of API protocols to meet specific use cases. Developers are encouraged to adopt a multi-protocol approach to optimize performance and maintainability.

---

[post]: <https://blog.postman.com/api-protocols-in-2023/>