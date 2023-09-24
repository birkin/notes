+++
title = "unicode urls"
date = 2023-02-03
description = "minimizing unicode gnashing of teeth"
authors = []

[taxonomies]
tags=[ "unicode", "good-practice" ]
+++


## The problem...

You're on top of unicode; you've even [normalized](https://github.com/birkin/dev_meetings/blob/main/2022/2022-01.md#unicode-trickiness) your filename containing unicode.

But you've given someone the url to that file, and then hear that the url doesn't work. They give you the url, and it looks like what you gave them, but doesn't work.

What's happened is that although the url you gave them contained the properly normalized unicode that _did_ work, they've saved the string you gave them in some way that undid the normalization.

## The solution...

Create a links that encodes the normalized form of the unicode.

The raw link will not be human-friendly, but it'll work, and the browser will show the nice-looking url.

Example:

You have a file named `birkin_iñtërnâtiønàlĭzætiФn_test.jpg`, properly normalized and saved on the server.

You need to supply the url.

You're tempted to show the url: 
`<https://some.edu/path/to/birkin_iñtërnâtiønàlĭzætiФn_test.jpg>`` -- which works in your testing.

Instead, provide the url:
```
<https://some.edu/path/to/birkin_in%CC%83te%CC%88rna%CC%82ti%C3%B8na%CC%80li%CC%86z%C3%A6ti%D0%A4n_test.jpg>
```

Yes, it looks horrible, but...

- you don't need to "show" that link
- when the user copies it into a browser, the browser will automatically show the nicer:
  `<https://some.edu/path/to/birkin_iñtërnâtiønàlĭzætiФn_test.jpg>``

Most importantly, the url won't get corrupted by whatever editor the user puts it through and will work when finally copied and pasted into a browser.

How to get that encoding?

- `from django.utils import http`
- `http.urlquote_plus( 'birkin_iñtërnâtiønàlĭzætiФn_test.jpg' )`
- ...which yields: 

```
birkin_in%CC%83te%CC%88rna%CC%82ti%C3%B8na%CC%80li%CC%86z%C3%A6ti%D0%A4n_test.jpg
```

- then use that in the full url above.
