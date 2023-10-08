+++
title = "shibboleth and fedora"
date = 2010-01-16
description = "a proposed Fedora authorization solution"
authors = []

[taxonomies]
tags=[ "authentication", "ideas", "repositories", "software development" ]
+++

_[2023 update -- our repository architecture has changed significantly (I'll post about it sometime), so this post (like so many old tech-posts) is for posterity. 🙂 ]_

---

I don't work directly on [Fedora][fedora_link] (our repository software), but am very familiar with it due to my work with a programmer who does, and because I've worked on a [django](http://www.djangoproject.com/) front-end for ingestion of items into fedora, as well as fedora-apis. My role in fedora work is more akin to the 'corner-man' in boxing. Together the boxer and I strategize about the opponent, his defenses and threats to our plans, and devise approaches to deal with evolving challenges. We cross ourselves, the fedora programmer goes into the ring, and between rounds I provide moral support, bandage wounds, and, because of my distance from actual battle, sometimes have useful ideas for the next round. This analogy's negativity toward the Fedora software is appropriate; to use another: We've bought a car that, in hindsight, I wouldn't recommend to others, but that we're committed to getting some terrific mileage out of.

[fedora_link]: http://en.wikipedia.org/wiki/Fedora_(software)

So, it's been a tough fight, but our boxer is quick, has impressive endurance, and we believe we'll come out on top.

Fedora authorization is one round in which we think we've scored well.

Fedora comes bundled with an authorization piece called [XACML](http://en.wikipedia.org/wiki/XACML). I don't know if it's due to xacml, or fedora's implementation of it, but from what I gather indirectly, it's terrifying enough that few use it, and it is, in fact, scheduled to be augmented in a future release with a new Great Hope: [FeSL](https://wiki.lyrasis.org/display/FEDORA34/FeSL+Authentication).

But if you want to go into production *now*, what to do? The dearth of published authentication/authorization 'live' solutions is why, as I understand it, so many fedora installations are either completely open (all objects public), or completely locked down for internal use.

We've assumed we would use some sort of wrapper around fedora, to authenticate against [Shibboleth](http://shibboleth.internet2.edu/), with which our university is slowly moving forward. Shib's lack of logout capability, and the resultant assumption that users will happily quit their browser to logout, would seem quaintly amusing if it weren't true -- but that is another topic entirely, and single sign-on is certainly convenient. Not long ago we began to tackle how, specifically, to implement shib/fedora authorization.

Recently someone described to me an authorization approach the [muradora](http://www.muradora.org/muradora) folk took. I haven't looked at any documentation myself, but I was told that they wrote a servlet filter that takes a submitted name and password, and passes it to a non-centralized custom ldap server that exists only for the purpose of allowing fedora's built in ldap-xacml code to handle authentication. (For those unfamiliar: a java servlet filter acts as a front layer of a java webapp through which incoming requests and outgoing responses must pass, and can be modified.) 

A few of us heard this and had divergent reactions. It sounded like a hack, which caused some to dismiss the approach. Personally, being quite partial to hacks that work around monolithic software obstacles, I thought the hack smacked of ingenious creativity and was worth further examination. I was indulged; the result: our corner has devised an approach that initial testing indicates will work well.

First, some necessary background info... 

* Our University shib implementation is integrated with [Grouper](http://www.internet2.edu/grouper/). I think grouper is, or at least historically has been, a separate project from shibboleth, but they work together brilliantly. Upon shib-login, a list of the groups to which the user belongs is accessible to the server via the shib 'is-member-of' header field.

* Our implementation of fedora item ingestion involves creating a [METS](http://en.wikipedia.org/wiki/METS) record that contains a bunch of item-info -- including a rights segment. The rights segment contains a series of entries, each one listing an identity (a shib is-member-of group) and a permission. Example (content, not format): identity='chemistry-department' & permission='view_item'

* The mets record is handed to an ingester that converts the mets xml to [FOXML](http://www.fedora-commons.org/download/2.0/userdocs/digitalobjects/introFOXML.html), then fedora grabs the object (we're using the 'managed' option at the moment), and the java messaging built into fedora fires off a message to a listener that indexes (via [Solr](http://lucene.apache.org/solr/)) parts of the foxml record, including the rights information.

So, our approach: create a fedora servlet filter that reads the shib groups/identities, then does a solr search to see if the object being requested has a 'view' permission for any of the identities in the request's shib is-member-of header. If so, the request is allowed through; if not; it is blocked. If no shib-identity is found, the servlet filter will only yield objects with 'public' view_item permissions. 

The beauty of this is that fedora-access can be fully open to the internet while still allowing authorized access for those objects that require it. Further, this solution offers reasonable hope that it will survive fedora upgrades, since the servlet, though a part of the fedora webapp, is somewhat of a separate layer in front of the app. Further, by adding more granular permissions (at the moment permissions are at the object-level; they could be at the data-stream level) -- or simply by a bit of extra programming in the servlet-filter -- we could allow, say, the public to access low and medium-resolution images, but allow, say, faculty to access high-resolution images.

*I'll keep this paragraph updated...* Our intrepid programmer has figured out where to insert the custom servlet filter, has worked with our systems person to hook up an initial apache/tomcat connection so as to allow the shib installation on apache to pass its headers through to tomcat, and confirmed the filter's detection of the shib identity header information. A nice side-effect of installing shib on apache rather than tomcat directly is that we can allow programmatic access to port 8080.

The bell has rung; the next round begins. We cross our fingers, and the programmer heads into the ring once again.
