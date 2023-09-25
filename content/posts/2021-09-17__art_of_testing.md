+++
title = "approaches to testing"
date = 2021-09-17
description = "acknowledging the pros and cons of approaches to testing"
authors = []

[taxonomies]
tags=[ "good-practices", "software-development", "testing" ]
+++

_The evolution of testing -- what's lost and gained?_

---

I have a project in which I'm parsing data.

One useful principle of testing is to have a discrete piece of functionality tested. And the most direct way to do that for parsing is to pass in source-data, and specify a clear assertion. 

## simple and direct

I began that way: 

[Here's](https://github.com/Brown-University-Library/parse_alma_annex_requests_code/blob/8109bdbf6b9ff3dd609d8d2c5c7775d72ad3de10/tests.py#L156) the beginning of Parser testing.

[Here's](https://github.com/Brown-University-Library/parse_alma_annex_requests_code/blob/8109bdbf6b9ff3dd609d8d2c5c7775d72ad3de10/tests.py#L241-L246) the first iteration of parsing a patron note -- although the test was originally called, simply `test_parse_patron_note()`.

That happened to be for a physical item; shortly thereafter I needed to parse the note for a digital item. [Here](https://github.com/Brown-University-Library/parse_alma_annex_requests_code/blob/8109bdbf6b9ff3dd609d8d2c5c7775d72ad3de10/tests.py#L248-L253) is the iteration that tested for that. 

Implementing that second test, I renamed the first example to show that the test was for a physical item, and named the second test to show that it was testing a digital item. I could have passed just the specific item-xml or item-xml-object to each test. In some ways that would have been simpler and "purer". But the real data for this project comes in a file containing multiple kinds of items, and I was going to be using the items for different kinds of tests (not just notes), so I figured I'd have one main test-file that would contain a variety of items to use for the tests. (Though this does add a slight dependency to the test -- file loading -- and dependences are frowned upon.)

In the two examples shown so far, I chose, from the [source-data](https://github.com/Brown-University-Library/parse_alma_annex_requests_code/blob/8109bdbf6b9ff3dd609d8d2c5c7775d72ad3de10/test_dirs/static_source/BUL_ANNEX-sample.xml) being tested, the [first list item](https://github.com/Brown-University-Library/parse_alma_annex_requests_code/blob/8109bdbf6b9ff3dd609d8d2c5c7775d72ad3de10/tests.py#L244) for the physical-note test, and the [sixth list item](https://github.com/Brown-University-Library/parse_alma_annex_requests_code/blob/8109bdbf6b9ff3dd609d8d2c5c7775d72ad3de10/tests.py#L251) for the digital-note test.

This is all reasonably forthright. The nice thing about this is that, coming back to this code in future weeks or months, and running the tests, I'd see from the terminal output, when running the test-suite, the explicit `test_parse_patron_note_physical()` and `test_parse_patron_note_digital()` tests. That's really useful when revisiting code.

But the more edge-cases that arise, the benefits of this explicitness quickly, for me, feel outweighed by the duplication. I could have half-a-dozen explicit tests for parsing just the notes field for physical items, another half-dozen for digital items, and have lots of very specific tests for all the other parsing.

## scalable

In this and other projects, in this situation, I've moved to a different pattern: a [single test](https://github.com/Brown-University-Library/parse_alma_annex_requests_code/blob/8109bdbf6b9ff3dd609d8d2c5c7775d72ad3de10/tests.py#L221-L239) for parsing the target field (in this case the note). This single test first loads up an array of items, an array of expectations, and then iterates through the array, so the single test in this case is actually testing eight variations.

This has some real advantages -- it's very scalable, since adding a new source-data item simply involves adding an expectation to this note, and the other parsed fields. I might be adding the new item because I'm aware of an edge-case for parsing, say, the item-barcode, and by having to also list the note expectation, I might end up catching some error I hadn't been aware of.

BUT... there is loss with the gain. I need to view the comments (or the source-data) to see/remember that I'm parsing physical vs digital items. (Might there be another digital item that I forgot to indicate via a comment?) And I'm not going to see those comments in the test-output. 

I just remembered long ago implementing something like this with an additional field in the array. Instead of just handing two-elements in each loop iteration (the source-item-data, and the expectation) -- I also had a comment that was printed, too. That would restore some of the useful specificity of output -- and on a failure, allow me to target, more quickly, the location of the error.

This example of gain/loss refactoring is a miniscule one -- but it reveals aspects of the decision-making in programming that I love.
