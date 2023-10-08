+++
title = "source of truth"
date = 2023-08-21
description = "what _is_ the source-of-truth data?"
authors = []
draft = false

[taxonomies]
tags=[ "code4lib", "repositories"  ]
+++

Just read a great post from long-time [code4libber][code4lib] Jonathan Rochkind: "[OCFL and ‘source of truth’ — two options][truth]".

To give a nutshell summary, it's first useful to be aware of a common web-development pattern, where the 'data' returned by a browser-request comes from an index. That index is an intermediary between the actual source data/file, and the webpage a user loads.

An example... For two work-projects, the source-truth of the scholarly data is in xml-files ([example][usep-example]). Knowedgeable trained folk encode data from headstones or other sources into these xml-files.  

But when a user performs a search on the project's webpage, or loads an inscription-page from the website, the server looks up info from our [solr][solr] indexer.

Why the intermediary index? Partly because indexers are very, very fast. Also because they can deliver great search results in a way that offers a user easy and useful ways to filter results (["facets"][facets]). And also because the most common indexers are very easy for developers to configure and query and update.

Given this small architectural tour, since the data for a web-request comes most directly from the index (not the xml files), it's easy to see how the "source-of-truth" _could_ be thought of as the index. If an xml-file hasn't been indexed, it won't appear on the website; in a way, it doesn't exist.

Jonathan's post focuses on a specification for saving files-and-associated-metadata to a filesystem, called [OCFL][OCFL] ("Oxford Common File Layout"). Though the uses of OCFL are not limited to repositories, it was developed from University repository-developers deliberating about, and implementing, a simple useful file-layout specification that different software-tools can use. 

Because OCFL is most common in this repository context, and because repositories conceptually prioritize archival durability, OCFL data tends to be thought of as "source of truth" data in repository-architecture. 

But repositories use indexers. Jonathan's post illuminates competing visions of whether the OCFL storage-layer, or the indexer (or some correlative intermediary) should be considered the "source of truth" -- and the implications for decisions. My take is a bit different than his about the increased technical challenges of an OCFL-first source-of-truth, vs an intermediary-first source-of-truth -- but the main take-away for me is that it's important to be very clear on what the purposes are for the two layers.

For the [BDR][BDR] (Brown Digital Repository), we want to ensure that if some disaster struck, and all the the BDR's infrastructure went down, but we still had the offsite-OCFL-file-data (and our indexer-code in GitHub), we could reconstitute the BDR.

But other projects may lend themselves to a _shared_ source-of-truth between the two key layers. 

For a current work project, the main data-source is a FileMaker-Pro database. That data is exported, and indexed; the website accesses the index. A long-term project is underway to scan this collection's materials, and put them in the BDR. Once there, we'll naturally want to link to the relevant BDR-content from the website. How to do that?

For various reasons, we've decided not to add BDR links to the FileMaker-Pro database. Instead, we'll add those urls directly to the index. So there will be very useful data in the index that's not in the foundational source-data.

But that's ok -- the important thing is to be clear and deliberate about what data is going where, for what reasons. And to be clear about how a useful website can be reconstituted from that source-data if needed. These are issues that we developers are _familiar_ with, but given time and resource constraints, may not always think through deeply and document clearly. Which is why I so appreciate Jonathan's post: it raises a variety of useful issues to work through intentionally.

[code4lib]: https://code4lib.org/ "code4lib.org link"

[truth]: https://bibwild.wordpress.com/2023/03/21/ocfl-and-source-of-truth-two-options/ "source of truth link"

[usep-example]: https://github.com/Brown-University-Library/usep-data/tree/master/xml_inscriptions/transcribed  "GitHub usep link"

[solr]: https://solr.apache.org/  "solr link"

[facets]: https://en.wikipedia.org/wiki/Faceted_search  "facet wikipedia link"

[OCFL]: https://ocfl.io/  "OCFL link"

[BDR]: https://repository.library.brown.edu/studio/  "BDR link"
