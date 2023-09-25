+++
title = "validating django params"
date = 2022-09-22
description = "suprises working on a solr-proxy"
authors = []

[taxonomies]
tags=[ "django", "good-practices" ]
+++

## expected a GET; got a POST

Some surprises while working on a recent [project](https://github.com/birkin/solr_proxy_project)...

I was creating a simple proxy-webapp to receive GETs, check the params against an allow-list, and pass on the cleaned params to query solr, returning json.

So my code [began](https://github.com/birkin/solr_proxy_project/blob/17ba0b68d2754b793c853fcf3a8507f55cef153f/solr_proxy_app/views.py#L48) by looking at the querystring.

Once I had everything working, and had checked a bunch of querystrings against it, I pointed the webapp calling solr to my proxy-webapp, and it didn't work.

Debugging took some time, because I was verifying what I knew, rather than being open to what I didn't know. I verified the params for the solr calls, ran them against my proxy-webapp, and it looked like it _should_ have been working. Turns out that the project calling solr was using an old library, [solrpy](https://pypi.org/project/solrpy/), which builds the select-data via POSTing form-like params to solr (using xml IIRC). Solr handles that just fine, but my proxy didn't, so I had to deal with the POST.

If I had to do this from the beginning, I'd start by looking at the params whether from a POST or GET, and should refactor to do that, but I had the code written (with tests), to expect a querystring, and to validate the params in the querystring, etc..., and was feeling a time-pressure, so I figured I'd just convert the POST params to a querystring and pass that querystring to the pre-existing code.

Did that, and then, when pointing the webapp to my proxy-webapp, _most_ things worked, but not all.

## querydict ≠ dict

That round of debugging also took some time, because whereas the original solr calls were all being made by python code, the solr calls that weren't working were being made by various javascript calls to a webapp-api (to avoid cross-site domain issues). Turns out the calls coming from javascript had lots of same-param fields. Here's an example:

```
q=*:*+AND+display_status:approved&facet.field=type&facet.field=physical_type&facet.field=language&facet.field=religion&facet.field=material&facet.field=placeMenu&indent=on&fl=type&start=0&rows=0&facet=on&wt=json
```

...there are six `facet.field` keys there.

My original convert-POST-to-GET code was treating the post-params as a regular dict (oops), and so was only passing one value to solr (since regular dicts don't allow multiple identical keys). I wanted to update the Django QueryDict (a Django dict-like structure that allows multiple identical keys) -- to validate the par, but the original django Querydict wasn't mutable, so I couldn't simply remove non-legit params.

So I made a copy (probably not in the most efficient way), and iterated through the original incoming Querydict's keys -- but actually updated the copy's params. Then, with the copy validated, I could return it urlencode() it and return it.

  My [implementation](https://github.com/birkin/solr_proxy_project/blob/17ba0b68d2754b793c853fcf3a8507f55cef153f/solr_proxy_app/lib/validator.py#L57).
