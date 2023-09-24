+++
title = "practical campus APIs & feeds"
date = 2008-02-16
description = "thoughts on APIs useful to Library users that would also benefit the whole campus"
authors = []

[taxonomies]
tags=[ "APIs" ]
+++

For a while now I've evangelized APIs & feeds, encouraging folk (and reminding myself) to to expose 'web-page' data by presenting it in some alternate structured format. That's partly for the purpose of making code-reuse a reality but even more-so for the purpose of making possible new and interesting uses of data.

At the Library, we've truly moved into the realm of moving code onto the network. The web-services we've created have, not surprisingly, been library-related:

- An isbn converter.
- A 'cleaner' for data output from an ILS API.
- Many 'tunnelers' into consortial borrowing services returning results of searches, with the order number, if applicable.
- A reprocessor of OCLC xISBN data that returns a only those OCLC xISBNS that have the same format and are in the same language as the submitted ISBN.
- An OCLC to ISBN converter that will take an OCLC number and see if there are versions of that item available with ISBNs.
- An OPAC status & location checker.
- etc. etc. etc.

I've wondered recently what APIs the library could offer that would be of value campus-wide. More specifically, what APIs we might develop for our own needs that would be useful to the campus as a whole. Of course, many of our APIs do currently benefit the wider campus community in that students, staff, and faculty across campus use services of ours that are made possible via our behind-the-scenes use of APIs. I'm thinking more of APIs that developers in other departments might find directly useful.

When considering APIs that would be useful for developers across the campus, I naturally think of our Computing and Information Services department (CIS). I've had good conversations, and hope to have many more in the future, with CIS folk about having them develop and evangelize campus-wide APIs. My thinking has been that over time, developing such APIs could save them an enormous amount of time as well as enhance good will from departmental developers.

An example: for one of our Library projects, we need a listing of faculty and course information. I'm not directly involved in this project, but my understanding is that we periodically request a list of faculty and courses from CIS; they produce the list; and we update some db tables for web-apps that make use of this information. My sense is that if certain Banner APIs could be enabled -- obviously with appropriate security implemented -- we could get this information directly from a feed / API call, simplifying our workflow and lightening the workflow of the CIS folk who produce the list for us.

I'm encouraged from my conversations that there are folk in CIS who share this perspective and are working to realize it. While good discussions and planning proceed, I find myself gravitating to what we in the Library could do *now* along these lines. Three ideas...

### Cafeteria menu

As part of an idea that deserves its own post (the idea sounds a bit silly without context, but indulge me), I've thought that it would be very useful on a particular Library web page to be able to display the next upcoming meal at the main campus cafeterias. I spent about ten minutes exploring the availability of that information, and found two web-pages and a downloadable excel spreadsheet. None of these are ideal sources of information to automate, but it could be done, and I wouldn't be at all surprised if the resulting structured feed would be of use to others, from individual students to the campus newspaper.

### SafeRide arrival time

We have a campus shuttle system comprised of about seven vans. A couple of these have GPS receivers, and a vendor website displays on a map _(map was linked; but no longer available)_, via quite gnarly javascript, the current location of the GPS-enabled vans. That's nice, but the experience could be significantly improved. 

I've thought it would be extremely useful to be able to display on a Library web-page (if the student is accessing the page from within the Library) a simple line like \"The next SafeRide shuttle should arrive here in about 10 minutes.\" Simple and seriously, wonderfully useful information, that doesn't get in the way of the task at hand. That same Library web-page, if accessed from outside of the Library, simply wouldn't have that line displayed.

The API we could create, from parsing the javascript on the vendor web-page, could most simply at a minimum return location information for the GPS-enabled shuttles, which could be interpreted by our own server-side logic to approximate arrival times. But even better, the logic of determining arrival times could be embedded in the API itself. The API could take a location-parameter and return expected arrival time for the submitted location. We at the library might only implement logic that focuses on the arrival times at the Library. But by opening up the arrival-assessment code, we could allow BioMed developers to add to add arrival-time logic for shuttle-stop-locations close to BioMed buildings, and students to add arrival-time logic for shuttle-stop-locations close to particular dorms.

Since developers can determine the IP address of an incoming request for information, and since developers and computer-knowledgeable students know the IP-address ranges of buildings in their purview, we really can do this.

### Public computer availability

Imagine you're a student. You need to get some good work done and *know* if you stay in your dorm room this evening you won't get that work done -- there are just too many distractions. So you want to go to the Library. You have a desktop computer, or maybe just don't feel like lugging your laptop in the rain, and you know the Libraries have public clusters. Problem is -- it's getting close to midterms and sometimes the clusters get pretty full. Wouldn't it be *great*, I mean, really, really great, to be able to access a web-page that shows public cluster availability across campus?

I've talked with some CIS folk about this and found individuals who are working hard to realize this goal. They do have software that can detect the 'in-use' status of each terminal in the clusters, and last I checked (in November, I think) had noted that the software had upgraded its web-display capability which with they were experimenting. However, the public web display of cluster availability is as of this writing only accessible... from cluster machines. But the hope is that this information will eventually be made more public. That's great, but I'd like to take the data a step further, and create an API to the data. The reason is that if the data were also exposed via an API in addition to a web-page, I could solve more specific problems in a targeted way. For instance, one of our Libraries has 15 floors, with public computers available on multiple floors. Wouldn't it be terrific if a student entering that Library could glance at a display screen and see the relevant computer availability (with floor numbers listed instead of generic cluster IDs) for just that building? An API would allow that.

I have other ideas as well, but this gives a good flavor of how in the future, as we meet Library needs, we might be able to offer very useful API data to developers across campus.

---

To close, an exhortation... In each of these three situations, I speak of creating an API from existing publicly available electronic data. My excitement about creating and then utilizing these APIs for user-services is evident. But really, I should not have to create the APIs; I should be able to spend my time building the useful services for the Library and our campus that the APIs allow. So to all: if you know anyone creating any web-information -- encourage that person to expose their data not only via a 'regular' web-page, but also in a predictable structured way that can make its re-use easy. And to anyone purchasing any vendor-service that offers electronic information, demand that the service offers an API to the data.