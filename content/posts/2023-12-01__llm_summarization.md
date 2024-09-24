+++
title = "llm summarization"

date = 2023-12-01
description = "using large-language-models for summarization"
authors = []
draft = false

[taxonomies]
tags=[ "AI", "code" ]
+++


### notes

- I did a bunch of googling and found that most summarization seemed to involved extracting actual-text segments that were representative of the overall document. This is even with newer code using large-language-models trained to be good for extraction. [Some experimental work](https://github.com/birkin/llm_summarizer_code).

- I didn't want that -- I instead wanted what we'd think of as summaries.

- I knew ChatGPT could do a fantastic job on this, and then remembered work some six-months ago I did on getting an open-source chat-oriented large-language-model running, for experimentation.

- I got that code running again, following a [video-tutorial](https://www.youtube.com/watch?v=-BidzsQYZM4), and [built on it](https://github.com/birkin/ml_llama_python_code) to experiment with using chat for summarization.
    - Interesting: when I tried that code six months ago, it worked pretty smoothly. But now, that model is old (the link 404ed). I had a hard time finding it, and the libraries that worked with it then no longer do (I had to downgrade to older versions). Shows how fast things are changing!

- Though I did get the [summary-of-summaries approach](https://github.com/birkin/ml_llama_python_code/blob/main/06_explores_summary_of_summaries.py) working, for the demo I switched back to a simpler approach of just summarizing the first 1,000 words.
    - for the demo, this produced good results, due to the maximum text often being handled due to everything being single-page scans.
    - i keep hearing that newer models are both better, and faster, and handle larger numbers of tokens -- so for the Hall-Hoag project, I may not use the summary-of-summaries approach -- except to experiment with organization-as-a-whole summarization.

- Note the prompt-experimentation for the [description-text](https://github.com/birkin/ml_llama_python_code/blob/762c0e2f27b39662b184c904249e217133ec11c4/07_temp_reversion_to_1000_words.py#L106-L109) -- and for [subtitle-text](https://github.com/birkin/ml_llama_python_code/blob/762c0e2f27b39662b184c904249e217133ec11c4/07_temp_reversion_to_1000_words.py#L110-L112).

- Note also meta experience of using a large-language-model to [explain the knobs](https://github.com/birkin/ml_llama_python_code/blob/762c0e2f27b39662b184c904249e217133ec11c4/07_temp_reversion_to_1000_words.py#L100) (parameters) for working with a large-language-model.  :)

---
