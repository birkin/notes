+++
title = "the wave and the repository"
date = 2009-11-11
description = "repository architecture thoughts inspired by Google Wave"
authors = []

[taxonomies]
tags=[ "ideas", "repositories" ]
+++

I've been playing with [Google Wave](http://wave.google.com) recently and am deeply impressed.

I would not be surprised if within a few years, a year for many, waves will largely replace emails. Not just for youth, whose primary forms of non-voice digital communication are sms-texts or facebook-posts, but also for those of us for whom email is currently an absolutely essential daily form of communication.

I believe it will be that significant.

For those not familiar with Google Wave, here are some links:

- [wikipedia entry](http://en.wikipedia.org/wiki/Google_Wave)
- Since you really have to see it in action, [here](http://www.youtube.com/watch?v=Itc4253kjhw) is an abridged version of the [1hr20min introduction](http://www.youtube.com/watch?v=v_UyVmITiYQ&feature=player_embedded)
- The [main site](http://wave.google.com/)

My mind-wheels have been spinning, envisioning what this new form of communication could impact.

## Library digital repository

At the [Access 2007](http://access2007.uvic.ca/?page_id=18) conference I saw an [inspiring talk](http://video.google.ca/videoplay?docid=6976320823933843470&hl=en-CA#) by Mark Leggott of the [University of Prince Edward Island](http://library.upei.ca/). He spoke about the [Virtual Research Environment](http://vre2.upei.ca/access2009/vre) that his group had created, which successfully addressed a thorny issue: Libraries which had  expended significant resources to build digital repository systems were having a terrible time getting campus entities to contribute content.

What was so compelling about Leggott's approach was his team's shift in perspective from expecting users to meet Library requirements -- to the Library meeting users' needs. I was still fairly new to the Library world at that time, but my sense was that institutions had built their digital repository to meet Library needs for thorough meta-data -- without much regard to user-experience or needs. The result: the new digital repository felt irrelevant to campus users. With onerous submission processes and requirements, little material was submitted. Leggott's team instead focused directly on useful services to key campus constituents such as faculty -- allowing them to more easily do the work they already did. As I recall, one simple example was that his group provided storage space for research data-sets -- but I believe the offer wasn't just for *final* data-sets, but data-sets under active development, revision, and analysis. The result: campus digital work worthy of inclusion into the repository was *already within* the UPEI Library system, which made final repository ingestion of appropriate material architecturally easy.

## Layering

Now that I have one work-foot in the digital repository world, I've been wondering about an issue stemming from my recollection of the Leggott team's approach: how to design a compelling suite of storage and easy-to-use services, without the Library repository being filled with vacation and pet pictures?

My thought: the Library could develop clear, simple policies for *layers* of repository-usage. The outer layer would be more flexible, more transactional, and would require a lower-level of quality metadata for submitted items -- tags would be fine. We already have a mission to support transactional, often non-archival work: supporting research. For items to be accepted into the inner more archival layer, more and higher quality metadata would be required, in exchange for the guarantee of permanence, multiple-channel data exposure, and format data-migration. The benefits of this layered approach: the Library can play an increased central role in the creative work of the campus, and ensure access to  quality data from across campus that would flow into the repository.

From this layering idea arises the question of how to architecturally separate the layers. Brainstorming, I've imagined that campus users could be allotted x00 GB of outer-layer 'work' storage-space -- with more inner-layer repository-space just a click away for items deemed appropriate. Or the outer-layer work space could be limited by time-frame: all files in the outer-layer workspace could have, say, a two-year lifespan, with a nice status-report system so no one would lose work unexpectedly. That'd help encourage worthy materials to be migrated into the inner layer.

## Leveraging

Recently, my thinking is shifting in a different direction. I still like the idea of an outer transactional work-layer, and an inner repository layer with richer metadata and higher archival guarantees. But I question whether we need to build all the outer-layer services. An alternate approach would be to facilitate the use of existing third-party services and tools, and build Library services, plugins, and widgets to streamline the ingestion of appropriate items from those external third-party work-layer services and tools.

My recent experimentation with Google Wave was a catalyst for this shift, especially given its collaborative strengths, and its ability to easily handle files and images via drag & drop.

## Vision

One of the use-cases we've envisioned for use of our digital repository is a professor organizing images for a class presentation. Imagine the professor is working with teaching assistants (TAs) to refine the presentation and associated points. With Google Wave, the professor could set up a wave to prepare for the class session. She could invite her two TAs into the wave; each could simply drag pictures into the wave, tagging them. The professor could also set up a bullet-point list in the wave, encourage the TAs to contribute to the bullet-list, and note issues for them to research in preparation for the class session.

Imagine if, when the session-material preparation is complete, the professor could then apply a Library repository-gadget to the wave which would, after a campus authentication process, ingest all the pictures and associated titles (and, optionally, the wave itself), and redirect the prof to a repository web-page to enter a bit more metadata. Upon adding this extra information, the data would be officially ingested into the repository. Because Google Wave is an open-source project, the Library or campus IT folk could, if desired, install a wave server to facilitate branding and make it all the easier for Libary services to be integrated seamlessly into users' work flow.

Google wave comes with an [Extensions](https://wave.google.com/help/wave/extensions.html) Gallery that provides inspiration for imagining the varied kinds of services that can be applied to a wave, and tutorials abound on [how to program extensions](http://googlewavedev.blogspot.com/2009/05/introducing-google-wave-apis-what-can.html). The same approach could be applied to flickr and facebook: Library programmers could build widgets and mini-apps to enable users to use friendly tools and services they're already comfortable with -- but to still be able to shift their works easily into the official repository. It's part of the idea of meeting users where they are, as opposed to requiring that they come to us. That this approach offers new and exciting realms for Library programmers is just delicious gravy.
