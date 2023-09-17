+++
title = "Moving code onto the network"
date = 2008-02-09
description = "Benefits of moving code from project-level classes and functions into a web-service."
authors = []

[taxonomies]
tags=[ "service-oriented-architecture" ]
+++

In 2004, while in my masters program, deeply immersed in java object-oriented programming, I saw the potential benefits of code re-use that classes offer. I envisioned over time building up libraries of class-objects; by accessing them in future projects, I expected to be more and more productive.

Code-reuse never quite worked out that way, though. What I've tended to do for new projects has been to copy a similar class from a previous project, paste it into the new project, weed out unnecessary attributes and methods, and add new code. In a way this makes sense: though I lose out on 'pure' code-reuse, I gain by having all code for a project together. That's nice for version-control and portability, and isolation of concerns in that I don't have to worry that a change in a class in one project will have unintended consequences in another project.

But reading a while back about service-oriented-architecture, and shortly thereafter having a need to code a couple of lines in python that I had just coded in php a day or two earlier -- the benefits of moving code into RESTful web-services, that is: moving it onto the network, became apparent.

I do that all the time now. Just last week I had a need to convert between 10 and 13-digit isbns -- for the second time in a recent project, so rather than coding the conversion directly in the program at hand I put it into a webservice.

In this shift, I've finally realized that goal of code reuse, while still being able to maintain the version-control and isolation of concerns benefits of focusing on my specific project at hand.

The book 'RESTful Web Services' by Richardson and Ruby, while a bit dense, offers good insights on creating web-services (example: versioning). At some point, I'd like to come up with standards for Brown Library (and/or campus-wide) web-services. Examples: specifying versioning in the url, a documention url in the returned data, and a url in that documentation of all APIs/web-services the department offers.

For now, though, the simple shift toward moving code out of individual projects and onto the network has been rewarding.
