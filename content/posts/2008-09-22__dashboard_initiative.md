+++
title = "dashboard initiative"
date = 2009-09-22
description = "notes on a dashboard idea"
authors = []

[taxonomies]
tags=[ "analytics", "presentation", "project" ]
+++


I've been putting some productive time into something I'm calling \"The Dashboard Initiative\". Most of this time to date has been outside of normal work hours due to a few other priorities, but in time I expect to add this to the list of on-going work projects.    
     
Inspired by work done by Brown's [Office of Institutional Research](http://www.brown.edu/Administration/Institutional_Research/), the concept of the dashboard is to provide useful trend information about the operation of different facets of the Library. The analogy to a car dashboard is good: whereas 'instruments' make up a car's dashboard, what I'm calling 'widgets' make up the Library's dashboard.    
     
As shown on this [dashboard information page](http://library.brown.edu/dashboard/info/), a dashboard widget consists of three counts (baseline, trend, and current), a trend indicator, and a 'more-info' button that itself is a miniature graph. My visions for possible future dashboard usage within the Library and across campus are grand, but it is important to remember that the dashboard idea is intended to serve a rather specific data-display purpose: to usefully display trend information. Data that lends itself to pie-chart breakdowns can be important to an organization and can be an integral part of an organization's data-farm, but is somewhat outside the scope of the dashboard focus on trends.    
     
One of the reasons I find the dashboard concept so compelling is that it provides a kind of 'template' for data-tracking feeds. Increasingly we've been building into more projects the ability to stream out statistic counts, but to date there hasn't been a clear standardized vision of how this statistical data might be presented. The dashboard offers that standard.     
     
If we were to rebuild from scratch the [easyBorrow](http://dl.lib.brown.edu/its/software/easyborrow/) system, we could from the start automate count-flows that could populate widgets representing trend-usage for Josiah redirects, BorrowDirect, VirtualCatalog, InRhode, and Iliad. This of course applies to all new systems, and over time I expect we'll retrofit many of our existing ad-hoc statistical counts to flow into widgets.    
     
I have a vision of the creation, over time, of a plethora of widgets representing useful trend-information on checkouts, interlibrary-loan usage, new-titles additions, collections-web-access usage, requests for offsite materials, and physical library attendance to name just a few. This then begs the question of how to manage all these widgets.     
     
I envision a 'MyWidgets' page where, based on cookies and login, a user could view a listing of all Library widgets, filter by tag, and select those she finds useful for a personalized widget page. As part of my work I may pay particular attention to the flow of easyBorrow requests to our different borrowing partners, and scan other widgets tracking workbench file uploads to our in-development repository. Other folk in the library might be particularly interested in widgets that track numbers of books sent to our offsite Annex facility, as well as widgets that track the number of requests for those materials, and widgets that track how many requests for offsite materials are still made when the user is offered a link to a Google Book scan of the requested title. Our French scholarly resources librarian might choose for her page widgets tracking French new-title additions, as well as checkouts of French-language items.    
     
Thinking even more broadly -- campus-wide -- it's easy to imagine how, if other departments adopt the dashboard idea, a facility could even be developed for, say, the chair of the French department to 'subscribe' to a Library 'French New-Titles' widget, a Library 'French-Language Checkouts' widget, as well as a Registrar widget representing the numbers of freshmen enrolled in French 1, and another Registrar widget representing numbers of French concentrators.    
     
Along these lines, I expect to one-day add an rss and html parameter-segment to a widget-url to facilitate such cross-campus usage.    
     
For now, starting on a small-scale, I've created via Django's default admin a simple form allowing non-technical end-users to create a widget simply by typing or pasting into the form a list of key-value data-pairs.     
     
![widget entry form](http://library.brown.edu/django_media/dashboard_media/images/form_sample.png)    
     
Upon submitting the form, the data-points are parsed  and made into the discrete data-elements comprising a widget. This is in-place now. In fact, the widget on the [dashboard information page](http://library.brown.edu/dashboard/info/) was created (and can easily be updated) via this form. Further, this weekend I implemented the ability to view detail line-chart information using [Google's chart API](http://code.google.com/apis/chart/). So changing a label or data-point via the simple form now changes not just the widget but also the detail chart, on-the-fly. Though I expect to automate many data flows used to create dashboard widgets, the utility of the form will allow non-technical folk to take data they already create via manual processes and easily make that data much more visible to others.    
     
We'll see how this all unfolds. The potential is exciting.    
     
*[ Update: I *[*presented*](http://code4lib.org/conference/2009/diana)* on the dashboard at the *[*2009 code4lib conference*](http://code4lib.org/conference/2009/schedule)*. Good feedback (*[*DC*](http://twitter.com/dchud/statuses/1245524571)*, *[*ELM*](http://infomotions.com/blog/2009/03/code4lib-conference-providence-rhode-island-2009/)*). ]*
