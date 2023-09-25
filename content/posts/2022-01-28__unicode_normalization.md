+++
title = "unicode normalization"
date = 2022-01-28
description = "paraphasing Montoya: 'I do not think this word is what you think it is.'"
authors = []

[taxonomies]
tags=[ "unicode", "good-practices" ]
+++

## The problem...

You feel you're on top of unicode, because all your database-data is encoded in utf-8, and your search-terms are encoded in utf-8, and internally you're decoding to unicode for everything -- all-good. But... you have a search term, and you _know_ the search term is in the database, yet no match is found!!

Example...

```
>>> database_words
['hola', 'más', 'qué']
>>> 
>>> 'foo' in database_words
False
>>> 
>>> 'hola' in database_words
True
>>> 
>>> 'más' in database_words  # search word typed in via mac 'option-e, a' method
True
>>> 
>>> 'qué' in database_words  # search word typed in via mac 'option-e, e' method
False  # ???
>>> 
```

The above confusing situation is because in the 'database' (`database_words`), the last word's accented-letter is two combined unicode-characters, but the search-term is using a single unicode-character for the accented letter.

Here's how `database_words` was created:

```
>>> database_words = ['hola', 'm' + '\u00e1' + 's', 'qu' + '\u0065' + '\u0301']
>>> database_words
['hola', 'más', 'qué']
```

And this is how you'd explicitly create the single unicode-character search term:

```
>>> 'qu' + '\u00e9'
'qué'
>>> 
```

(On the Mac, that accented-e is created via typing `option-e` then `e`, which produces the above single-unicode character.)

There is no way, just by looking, that you can tell the true nature of that accented 'e'.


## examining characters, if curious...

```
>>> import unicodedata
>>> 
>>> for c in 'qué':  # typed in via option-e method which produces `'qu' + '\u00e9'`
...     print( f'unicode-name, ``{unicodedata.name(c)}``' )
... 
unicode-name, ``LATIN SMALL LETTER Q``
unicode-name, ``LATIN SMALL LETTER U``
unicode-name, ``LATIN SMALL LETTER E WITH ACUTE``
>>> 

>>> for c in 'qué':  # pasted in from database_words, which uses the two combined unicode-characters: `'qu' + '\u0065' + '\u0301'`
...     print( f'unicode-name, ``{unicodedata.name(c)}``' )
... 
unicode-name, ``LATIN SMALL LETTER Q``
unicode-name, ``LATIN SMALL LETTER U``
unicode-name, ``LATIN SMALL LETTER E``
unicode-name, ``COMBINING ACUTE ACCENT``
>>> 
```

## Dealing with this weird reality...

_Good tools, like solr, often enable you to not have to worry about this -- a search-term with characters composed one way will generally find content composed the other way._

If you normalize-->decompose data in the database, and normalize-->decompose the search term, all will work.

The code below normalizes by decomposing single-unicode characters into multiple-unicode characters. Note that we start with the single unicode-character, and transform it into the two combined unicode-characters.

```
>>> decomposed_output = unicodedata.normalize( 'NFKD', 'qu' + '\u00e9' )
>>> 
>>> for c in decomposed_output:
...     print( f'unicode-name, ``{unicodedata.name(c)}``' )
... 
unicode-name, ``LATIN SMALL LETTER Q``
unicode-name, ``LATIN SMALL LETTER U``
unicode-name, ``LATIN SMALL LETTER E``
unicode-name, ``COMBINING ACUTE ACCENT``
>>> 
```

## So one overall solution... 

Save data in a normalized-->decomposed way...

```
>>> decomposed_database_words = []
>>> 
>>> for word in database_words:
...     decomposed_word = unicodedata.normalize( 'NFKD', word )
...     decomposed_database_words.append( decomposed_word )
... 
>>> decomposed_database_words
['hola', 'más', 'qué']
>>> 
```

...and then normalize-->decompose the search-term...

```
>>> search_term = 'qu' + '\u00e9'  # demonstrates search term starts with the single unicode character
>>> 
>>> decomposed_search_term = unicodedata.normalize( 'NFKD', search_term )
>>>
```

...then the normalized-->decomposed search term will find the data...

```
>>> decomposed_search_term in decomposed_database_words
True
>>> 
```
