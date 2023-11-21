+++
title = "ai4Libraries virtual-conference"

date = 2023-10-26
description = "quick notes"
authors = []
draft = false

[taxonomies]
tags=[ "AI", "conferences" ]
+++


### conference info
- virtual conference, October 19, 2023
- [org](https://www.ai4libraries.org/)
- [recordings](https://www.ai4libraries.org/2023recordings)

---

### take-aways

#### Morning keynote by Dave Hansen
- _terrific_
- Some issues around mining-for-AI aren't new, legally; text-data-mining has been around for a long time.
- _lots_ of lawsuits recently filed (against Stability, OpenAI, Meta) -- should have more clarity over the next year or so
- Is it permissible to use copyrighted works for use as training data? -- for non-commercial academic-research, probably, based on text-mining settled law.
- Open questions:
    - what about when copying is't just for search/analysis, but for creation of new works?
    - how should we think about systems that are used by users to create new works that may in some way substitute for the original?
    - "snoopy problem" -- generative AI can be used to create known-copyrighted-characters.
        - do the products/tools have safeguards _against_ creating copyrighted outputs? If not, does that put the tools and tool-creators at legal risk?
        - to what extent are the products/tools (vs user) responsible for resultant infringing works?
- Terms of service can have implications.

#### AI, Libraries, and Higher Education (Panel
- AI tools will play a role in retrieval of info. Either because users want to use them, or because regular tools we all use will begin invisibly using AI.
- Libraries have a historic curation role -- offering not only the info but info but also attributions of where info is from -- unlike AI.
- Some AI tools are _super_ useful for academic-research projects -- eg fingerprinting project.
- Fit technology to goals -- good calculator analogy: if the purpose is "learning arithmetic", don't use calculator much. But if it's learning higher-level calculus, a calculator is essential.
- Our ways of knowing / demonstrating-knowledge --  have been through writing. Now that writing is easy and cheap and not necessarily connected to a human author, writing may be less valuable.
- One aspect of protecting ourselves from copyright infringement is to clarify that AI-use is educational/for-learning -- not commercial.
- Assertion for good discussion: _"AI won't replace humans, but humans with AI will replace humans without AI."_

#### AI and Ethics: Considerations for the Scholarly Communities
(points below are a mix of points made and my thoughts)
- Should it be clear that presented data may have been (partially) AI generated?
- Should our resources be permitted to be harvested for AI?
- How to keep AI tools from harvesting user-info potentially inappropriately?

#### Trends in Challenges in Generative AI Adoption in Higher Education
(points below are a mix of points made and my thoughts)
- Ithaka S+R is working on an AI-Resiliency project, with 19 universities
    - because I never remember: the "S+R" stands for "Strategy & Research"
- Areas AI will be affecting: search, collections-as-data, process-automation, analytics, smart-sensors.
- Sandboxing one technique to minimize PII leakage. One example mentioned in chat: <https://gpt4all.io/index.html>

#### Tech-Services panel
(points below are a mix of points made and my thoughts)
- Examples of how back-end processes are and will be affected by AI: transcriptions, OCR, using AI to write scripts, auto keyword-generation, enhancing OpenRefine-ish capabilities; auto-cataloging to MARC-format.
- Defining licensing-protections should be a goal; challenging.
- Challenge of communicating Library desires to vendors. They may be receptive, but if the main point-of-contact is salespeople, not constructive.
- Conveying that AI is basically "statistical guessing" may reduce staff fear.
- Would be nice to investigate ways staff knowledge could be used to train tools.

#### Lightning talks
- __Leveraging AI tools for automating metadata extraction__ -- UCLA folk used OCR, fed data into spaCy for "named entity recognition", tried using chatgpt for DC records (good for title, description, language; bad for date, type, physical description, rights)
- __Moles and Martians: A New, LLM-based Library Search__, by Tim Spalding, LibraryThing -- gave examples of human exploratory searches that were handled well. See <https://www.talpa.ai> and the youtube video there.

---

### interesting projects/articles mentioned
- "[The DataSitters Club](https://datasittersclub.github.io/site/)"; group at U.Richmond doing interesting work on "distant-viewing" -- analyzing characters in Bewitched & I Dream of Jeannie
- "[A Very Gentle Introduction to Large Language Models without the Hype](ttps://mark-riedl.medium.com/a-very-gentle-introduction-to-large-language-models-without-the-hype-5f67941fa59e)" 
- "[Contrastive Attention Networks for Attribution of Early Modern Print](https://arxiv.org/pdf/2306.07998.pdf)"
    - summary: _The study develops a machine learning method to identify printers of early modern English books by analyzing damaged type-imprints in anonymous prints. Using a novel Contrastive Attention-based approach and synthetic data generation, the technique effectively matches type-imprints, aiding in historical print attribution._ (ChatGPT4)
- "[ChatGPT in Education: Partner or pariah?](https://dl.acm.org/doi/pdf/10.1145/3589651)"
- "[AI chatbots can infer an alarming amount of info about you from your responses](https://arstechnica.com/ai/2023/10/ai-chatbots-can-infer-an-alarming-amount-of-info-about-you-from-your-responses/)"
- "[Making AI Generative for Higher Education](https://sr.ithaka.org/blog/making-ai-generative-for-higher-education/)"
- "[...magical, AI-powered library search backed by true and authoritative data...](https://www.talpa.ai)"
    - summary: _Talpa is an AI-based library search tool, integrating Claude AI, ChatGPT, and authoritative book databases. It provides accurate, library-specific search results, currently free for certain libraries. Developed by LibraryThing, in collaboration with ProQuest, Talpa is an ongoing experiment​​​​​​​​​​._ (ChatGPT4)

---