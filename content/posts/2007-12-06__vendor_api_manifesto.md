+++
title = "Vendor API Manifesto"
date = 2007-12-06
description = "all vendor products should offer APIs -- period"
authors = []

[taxonomies]
tags=[ "APIs" ]
+++

*(I wrote this early in the Fall of 2007 and circulated it to folk in the Library who were attending meetings at which vendors were advertising their wares.)* 

---

Software products are created, understandably, primarily to meet existing needs. There are varied bodies of thought as to how much a software product should be designed to meet 'future possible needs'.

At certain points in recent history, it may have been reasonable to design the sole interface to a system assuming that the user of the interface would be a person using a web-browser.

Though APIs (application programming interface) have been around for ages, the trend toward programmers wanting to access internal and external systems via APIs has accelerated tremendously over the last few years.[*] As a programmer for a creative web-services department in a creative Library, I'm part of this trend. Our team's need to be able to programmatically access systems has increased dramatically. Fortunately, a few vendors such as Ex Libris understand this and have built possibilities for programmatic access into their products. But many closed systems remain.

To managers and directors making purchasing decisions, I urge that a *top-level* purchasing consideration be whether the vendor's product offers an API to the information it provides (in addition to any built-in web interface). The simple reason is that a web presentation of information is designed for a single purpose: for a user to interact with the system via a browser. An API allows the system's data to be accessed in any way we see fit, now or in the future.

A concrete example for any reader not familiar with the notion of an API...

Our team is currently developing a system to simplify the process of obtaining a book through interlibrary-loan services. In order to do this we have been able to automate the process of searching a consortial web-catalog for an item, and requesting that item. But the only method of doing this involves creating a program which essentially mimics a browser, automatically simulating clicked buttons and links and reading the resulting HTML of the consortial catalog's web interface.

This works, but is terribly fragile: if the design of a web-page changes, our program may no longer work until it is reconfigured to understand the new design.

What we absolutely need (in addition to the existing web interface) is a catalog-service (the API) which would allow a defined http request to be sent to a URL that will allow a search to be performed, or an item to be requested, etc. (That http request would come from a program our team has written -- instead of from a user sitting at a browser.) Each request to this API would return predictable documented structured information (XML is one standard; there are others). Our team's program would then be able to automatically process this information.

It is worth emphasizing that I am not asking for a 'whole new program' from the catalog vendor. A system's existing internal program logic that produces the information for the regular web data-stream is applicable to production of the alternate API data-stream. Yes, it takes thought and work to create a good and secure API and document it -- but an API, essentially, presents the same data as a web interface, in a simpler format. The mind-shift in offering an API is often larger than the work-shift.

Finally, about interacting with vendors regarding this issue... Vendor sales people aren't the developers, and it sounds like I am asking for something that vendor developers would be more knowledgeable about. But I've seen different vendor sales representatives at workshops and conferences, and the representatives for products that provide APIs have universally very clearly understood the importance of this issue. Thus if a product representative does not seem to understand this important feature, I would have significant concerns with the product.

---

Notes...

[*] Key aspects of this trend are articulated in the seminal article ["What Is Web 2.0 --
Design Patterns and Business Models for the Next Generation of Software"](http://www.oreillynet.com/pub/a/oreilly/tim/news/2005/09/30/what-is-web-20.html) by Tim O'Reilly.