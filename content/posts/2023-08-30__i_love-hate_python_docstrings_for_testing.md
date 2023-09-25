+++
title = "docstring-testing: love→hate→forget→rediscover→repeat"

date = 2023-08-30
description = "❤️ i've just rediscovered them ❤️"
authors = []
draft = false

[taxonomies]
tags=[ "code", "testing" ]
+++

I have a love-hate relationship with [using python docstrings for testing](https://realpython.com/python-doctest/). They're simple, easy-to-use, and provide both usage-documentation and actual unit-test functionality. But whenever I start using them in any serious extensive way, I go back to using regular unit-tests in a file or directory -- because of limitations of docstring-tests. So I haven't used them in a while. But for a informal collaborative experimental project, without testing set up, today I wanted to add a few simple tests to a function to confirm that it's really doing what we expect. I remembered docstrings for testing, and I'm once-again in the love-phase.

[Here's a function](https://github.com/Brown-University-Library/ml_bdr_ota_experiment/blob/0a9c4f0fc7a3471736a7344b6e441274bf61d2dd/data_clean.py#L122) in some experimental code a few of us are working on -- to which I added a few docstring-tests. The docstring is everything between the initial and closing `"""`. Generally docstrings are just used to comment a function. But they're cool for two reasons:

- tools such as Sphinx can be run on code to auto-generate documentation from docstrings. (I never use that.)

- assertions can be auto-executed as tests. 

In this function, [here are the doc-test assertions](https://github.com/Brown-University-Library/ml_bdr_ota_experiment/blob/0a9c4f0fc7a3471736a7344b6e441274bf61d2dd/data_clean.py#L127-L134). If the project had a normal unit-test harness, running tests the regular way would not only run the unit-tests, but also automatically test these assertion-statements. This experimental code has no test-harness set up; there are no unit-test imports. But the docstring tests can still be run like this: `% python -m doctest ./data_clean.py`

Doing that shows no output if the tests pass (you would see lots of output if running with the `-v` (verbose) flag). But imagine if the part that reads:

```python
    >>> stringify_list( 42 )
    '42'
```

...instead were:

```python
    >>> stringify_list( 42 )
    'blah'
```

...then, running the test would yield:

```python
**********************************************************************
File "/path/to/ml_OTA_experiment_stuff/ml_bdr_ota_experiment/./data_clean.py", line 133, in data_clean.stringify_list
Failed example:
    stringify_list( 42 )
Expected:
    'blah'
Got:
    '42'
**********************************************************************
1 items had failures:
   1 of   4 in data_clean.stringify_list
***Test Failed*** 1 failures.
```

Cool -- simple lightweight documentation and testing; very nice!
