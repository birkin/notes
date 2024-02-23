+++
title = "applying stylesheets"

date = 2023-11-11
description = "code-recipe for applying a stylesheet"
authors = []
draft = false

[taxonomies]
tags=[ "code" ]
+++


### small focused `how-to`

For a project with some xml-content, I put together a little demo of using python to transform a [source xml file] containing a dummy list of fifteen test-entries (three people with five entries each) like this...

```xml
[snip]
<TestEntries>
    <!-- Entries for Person 1 -->
    <Entry>
        <PersonName>Person 1</PersonName>
        <Date>2023-01-01</Date>
        <TestScore>85</TestScore>
    </Entry>
    <Entry>
        <PersonName>Person 1</PersonName>
        <Date>2023-01-15</Date>
        <TestScore>88</TestScore>
    </Entry>
[snip]
```

 -- into a nice summarization (with test-scores averaged), like this...

 ``` xml
 <scores>
  <Person>
    <Name>Person 1</Name>
    <average>83.8</average>
  </Person>
  <Person>
    <Name>Person 2</Name>
    <average>87.0</average>
  </Person>
  <Person>
    <Name>Person 3</Name>
    <average>84.0</average>
  </Person>
</scores>
 ```
 
...by [applying] a stylesheet.

[source xml file]: <https://github.com/Brown-University-Library/xslt_exploration/blob/759fd00c06bfa2833fc60129c85665a2ffe5ad84/source_files/source.xml>

[applying]: <https://github.com/Brown-University-Library/xslt_exploration/blob/759fd00c06bfa2833fc60129c85665a2ffe5ad84/transform_code.py#L38-L50>

### recipe thought

It'd be useful over time to build out a list of `recipes` for either good-practices or for small focused how-tos. GitHub's ability to link to a line or lines means that an index of recipes could reference small parts of existing projects -- or small focused repos such as this.

---
