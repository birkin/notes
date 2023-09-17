+++
title = "user context"
date = 2007-12-06
description = "customizing the user experience based on user context"
authors = []

[taxonomies]
tags = [ "user-context" ]
+++


I recently organized a meeting to brainstorm about what kinds of cool library things we could do if we knew more about a user's context. I also put up a wiki-page[1] for the brainstorming process.

This stems from a requirement for a project: I had to be able to access a particular barcode related to a user. Turned out the only way of getting at this barcode was to first get another piece of information, and then use that first piece of information to call an API that returns a bunch of info about a user, including the barcode. Fine; did that; got the barcode and used it for a tunneler I built. I then went to the [Access 2007 conference](http://web.archive.org/web/20130113222506/http://access2007.uvic.ca/?p=32), a wonderful library programming/technology conference, where, among other terrific presentations, I heard Mark Leggot speak[2] about the repository [presentation-PDF](http://loomware.typepad.com/docs/Repository_Redux_PubVersion.pdf) he set up at the University of Prince Edward Island (UPEI). He mentioned the importance of understanding a user's 'context'. Something clicked, and the general implications of what our team had achieved by being able to tie a user's log-in to this API-info about the user became clear.

This is nothing new in the internet business world; Amazon has been trailblazing this path for years. But given that authentication has mostly been a simple 'boolean' system in our Library webapps of just determining whether or not a user is permitted to access a site -- this opens up worlds of exciting possibilities. Already we've implemented a proof-of-concept 'drop box' that determines, from login, the user's 'type' (faculty/staff/student) and department and uses this data to customize the page displayed after login. Exciting stuff!

---

Notes...

[1] The University's Confluence wiki was retired; the reference was: `https://wiki.brown.edu/confluence/display/library/User-context+brainstorming`

[2] The video of Mark Leggot's presentation is no longer available; the reference was: `http://video.google.ca/videoplay?docid=6976320823933843470&hl=en-CA`