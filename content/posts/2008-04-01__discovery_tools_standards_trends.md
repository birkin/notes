+++
title = "discovery tools, standards, trends"
date = 2008-04-01
description = "report on the March 2008 NISO discovery forum."
authors = []

[taxonomies]
tags=[ "conferences", "presentations" ]
+++

*[Got a nice little blog-recognition email a couple weeks ago by a reader asking if I would write up a report on this NISO conference for possible inclusion in a newsletter. Here's the web-version.]*

---

Thirteen presentations were given at the [NISO](http://www.niso.org/home) Forum ['Next Generation Discovery: New Tools, Aging Standards'](https://www.niso.org/events/2008/03/next-generation-discovery-tools-new-tools-aging-standards), held on March 27 and 28, 2008, in Chapel Hill, North Carolina. They covered three main areas: current user-expectations, discovery tools attempting to meet those expectations, and architectures to facilitate the development and adoption of discovery tools.

Speakers reenforced that users want searching to be easy and fast. Dinah Sanders of III noted how this process of finding information has become increasingly iterative, with users expecting to refine their queries. Vinod Chachra of VTLS described that this is why search results must be returned quickly: it allows humans to be seamlessly involved in the discernment process, scanning and instantaneously determining relevancy.

Robert Sandusky of the University of Illinois at Chicago, Cameilia Csora of 2collab.com, Karen Hawkins of scitopio.org, Dinah, and Peter Murray of OhioLINK, all showed tools that incorporate at least some now-common web elements to meet these user-expectations, including faceted results, tagging, tag-clouds, and feeds.

Many new discovery tools offer truly laudable interface-improvements over previous displays of information, but suffer from a significant architectural limitation: If a tool assumes the only end-user experience is the tool's default web-page, opportunities for discovery are drastically limited. For example, if we at Brown were to license the III Encore tool, and a user were to land on one of our ['Napoleonic Satires'](https://library.brown.edu/cds/napoleon/) collection pages, it would be wonderful to be able to query an Encore API on 'Napoleon' to display in a sidebar the terrific discovery data this tool can access. But this and many other discovery tools offer no such API. Fortunately this is changing, with some vendors updating their business models to meet current library discovery needs both deeply and broadly. Ex Libris' [XServer](https://knowledge.exlibrisgroup.com/MetaLib/Knowledge_Articles/Documentation_on_X-server_MetaLib_Version_3.13_and_Higher) licensing is a prime example, offering API functionality to its federated-searching tool, dramatically broadening discovery possibilities beyond the default MetaLib web interface.

The presentations that touched on system-design and architectural issues to improve discovery were particularly inspiring. 

Richard Akerman of NRC CISTI noted that we should utilize our power as information-producers to produce data that more easily lends itself to machine-harvesting. This can be done by encoding data where possible utilizing existing standards such as [OpenURL](http://en.wikipedia.org/wiki/Openurl) and [COinS](http://en.wikipedia.org/wiki/COinS), as well as emerging de-facto standards such as [microformats](http://en.wikipedia.org/wiki/Microformats). He showed as one example information displayed in a useful time-line format by a site that had queried data from a harvester site -- possible because of standardized structured date-fields.

Mike Teets of OCLC gave a presentation on OCLC's emerging [WorldCat Grid](http://worldcat.org/devnet/blog/presentations/2008_01_ALA_Grid_Intro.pdf) services, offering possibilities for cross-referencing standard identifiers such as ISBNs and OCLC numbers, and emerging identifiers such as 'identities' -- truly a developer's dream.

Vinod offered numerous useful suggestions for designing systems to minimize user confusion and maximize utility. He showed an example of a site that had both a facet category of LC Subject Headings, and another facet category of Dewey Subject Headings, and the ease with which a user could be confused by this explicit display of overlapping information, hindering rather than helping discovery. 

Michael Winkler of the University of Pennsylvania discussed how [PennTags](http://tags.library.upenn.edu/help/) is emblematic of an architectural approach the UPenn Library has found successful. His talk brought together multiple threads of this NISO Forum by showing how PennTags offers discovery possibilities in multiple different settings because it is designed as what he called a 'horizontal' service, as opposed to a 'vertical' service. The 'vertical' service paradigm in Winkler's view is exactly the one I described earlier as architecturally limited: much useful information is gathered together and funneled down into one website with no possibilities for alternate exposure of the gathered and massaged data. PennTags, he noted, is an example of the 'horizontal' service paradigm that he sees as the future of UPenn Library discovery software and good discovery software in general. It is not tied to any particular existing service: not the catalog, not electronic resources, not their course-software -- and yet can be used with any of these services -- and in any given context can expose interesting data from another context. Each PennTag entry is exposed as an RSS feed which illustrates the power of simple standards to enhance discovery. In fact, this shift to a horizontal paradigm is so central to the UPenn Library's current and future work, that Winkler noted he toyed with re-titling his presentation to something like 'Not PennTags, but Why'.

John Mark Ockerbloom, also of the University of Pennsylvania, followed with an update on the DLF's ['ILS Discovery Interface Task Force'](http://code4lib.org/conference/2008/lynema), of which he is the Chair. The task force is set to soon release a standard for ILS discovery services -- in other words, it will set a lightweight API standard for the OPAC layer of the ILS. In the context of this forum, this standard should help foster the shift of the OPAC from a vertical silo-service to a horizontal more flexible one, increasing opportunities for discovery of the underlying OPAC data.

I hope to see the next Forum in this 'Discovery' series showcase more tools that utilize Winkler's horizontal-service architecture concept that increases discovery possibilities. Kudos to NISO for providing another thought-provoking Forum packed with inspirational examples and ideas and conversation.

Links to presentations should be available soon from the NISO [event website](https://www.niso.org/events/2008/03/next-generation-discovery-tools-new-tools-aging-standards).