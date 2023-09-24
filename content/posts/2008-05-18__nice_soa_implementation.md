+++
title = "nice lightweight SOA implementation"
date = 2008-05-18
description = "some good API practices"
authors = []

[taxonomies]
tags=[ "APIs", "service-oriented-architecture", "good-practices" ]
+++

I've evangelized [service-oriented architecture](http://en.wikipedia.org/wiki/Service-oriented_architecture) (SOA) [before](@/posts/2008-02-09__moving_code_onto_network.md). 

To review, briefly and roughly: SOA promotes decoupled services. For example, a Fahrenheit-to-Celsius converter would likely be implemented as a web-service, instead of as a function/method embedded/tied into some bigger program. The benefits of this are multiple: 1) The service can be written in any programming language, and accessed by other services written in different languages. 2) SOA makes the idealized promise of code-reuse a reality.

I have a programmer friend who works for a large corporation who is familiar with implementing SOA using industrial-scale best-practices; I'm familiar with implementing it in a lightweight, seat-of-the-pants fashion.

Over the past year+ I've created well over a dozen or so SOA web-services for different projects. But I recently implemented one I put some best-practice effort into that'll be a model for my future SOA work. Some links:

_[2023 update -- the march of progress has resulted in the retirement of these services, so no active links. Sorry!]_

`http://library.brown.edu/services/language_translator/`
`http://library.brown.edu/services/language_translator/api_v1/code_eng/`
`http://library.brown.edu/services/language_translator/api_v1/all/`
`http://library.brown.edu/services/language_translator/list/`

What I like about this one...

- The api urls offer 'discovery' via embedding, in the built-in returned data, contact and documentation information. Having just one of these pieces of info would be great; having both is particularly nice because web urls and staff change over time. Why is this useful? If someone is looking at the code that calls this service 5 years from now, and if I'm not around, the documentation will provide info on some extra features of the service that otherwise wouldn't be apparent if, say, the web-service just returned the word 'English'

- The api urls are 'hackable', another way of enhancing discovery. One can intuitively try entering a code other than 'enk' to see what comes up (like '[tlh](http://library.brown.edu/services/language_translator/api_v1/code_tlh/)'). Also, reasonably appropriate things happen if one lops off increasing sections of the url (in this case, redirects to documentation pages).

- The api urls are versioned. Key:value pairs can be added to this api -- but the existing key:value pairs must never be changed. The reason is that post-release, I don't know who's using it for what, thus I have to assume any changes could break someone's app. So if I want to change the label 'response' to 'language', and deliver it in xml, I can leave the existing one as is, and label the new one 'api_v2'.

- All these urls utilize server-caching. This is an implementation rather than a design feature, but worth mentioning. [Django](http://www.djangoproject.com/) offers a flexible and easy-to-use [caching feature](http://www.djangoproject.com/documentation/cache/); I have it set so that the list and api urls only have to hit the database once a day, no matter how many times the urls are hit. Further, django's caching is intelligent: its response includes 'Cache-Control', 'Etag', and 'Expires' http-headers so that a browser or well-designed code *doesn't even have to call the web-service again* to redisplay the data. Nice. This would be particularly important and useful for something like RSS feeds. 

Good info...

* A terrific, hands-on review-resource on http-headers: The [web-services chapter](http://www.diveintopython.org/http_web_services/index.html) of Mark Pilgrims 'Dive Into Python' [website](http://www.diveintopython.org/index.html) & [book](http://www.worldcat.org/oclc/56366433).

* Many of the features of this language_translator web-service were informed by the [book](http://www.worldcat.org/oclc/82671871) 'RESTful Web Services', by Richardson & Ruby. Some parts are a bit dense, but it's chock-full of terrific detailed info and food for thought. I came across it after having written a half-dozen or so SOA web-services, each one a little different and better, and it directly addressed many issues I had begun to think about or saw referenced via web-research.

*[Acknowledgements to Peter Murray's* [*article*](http://dltj.org/article/defining-soa-by-analogy/) *and Richard Akerman's Access_2006* [*presentation*](http://scilib.typepad.com/science_library_pad/access2006/) *that first inspired my SOA thinking.]*
