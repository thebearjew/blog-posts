---
layout: post
title: Natural Language Processing Fundamentals with Prof. John DeNero
date: 2015-04-06 16:10:14
published: true
---

![The Talk]({{ "nlp-denero-1.jpg" | prepend: site.images_path }})

All of us have done something like this: *Google Translate* > *"Hello"* > *Translate to Dutch* > *Paste*, but give little thought to what process is doing all of the work.
<!-- more -->

Many of our initial assumptions about Human-Computer Interactions are naive. A young child might explain this process as "*someone must have entered the dictionary into a computer and that's how we get translations*". While true, there are far more steps required in order to accurate decompose then interpret sentences.

This is exactly what Professor John DeNero talked about at Berkeley's Cloyne CO-OP on March 18th. DeNero teaches the most popular Berkeley class: [61A](http://cs61a.org).

I decided to attend this event after a Facebook invitation from [Hackers@Berkeley](http://hackersatberkeley.com). I had no idea that DeNero had such a proficient background in the subject until right before the event. I found out that before his current position, Professor DeNero was a [researcher](http://research.google.com/pubs/author38952.html) at Google. He worked specifically on [Google Translate](https://translate.google.com) and Natural Language Processing.


### Natural Language Processing

Quickly... what the hell is it? From [Wikipedia](http://en.wikipedia.org/wiki/Natural_language_processing):

> Natural language processing (NLP) is a field of computer science, artificial intelligence, and linguistics concerned with the interactions between computers and human (natural) languages
> [...] challenges in NLP involve natural language understanding, that is, enabling computers to derive meaning from human or natural language input, and others involve natural language generation.

Basically, make computer understand what *we*, humans say (not what binary says) and communicate back in our paradigms of language.

To address this, he opened with this simple sentence...

> Programs must be written for people to read

Besides being a relevant concept in Computer Science, it can be interpreted and broken up in many ways. Each word has an isolated meaning which is the simplest and an implied meaning in context of the other words. For example "programs" can be any of these 

![definitions]({{ "syntactic-ambiguity.png" | prepend: site.images_path }})

Or the sentence can be taken as "Programs must be written. For people to read". Such that people will be illiterate unless programs are written.

This context, which DeNero humorously brought up, can be the difference between a completely coherent sentence and one of bizarre possibilities. Take these headlines he provided:

> Stolen Painting Found by Tree

Depending on one's interpretation, a response could be "wonderful!" or... "thank you tree."

One more...

> Children Make Nutritious Snacks

ಠ_ಠ

### The Problem

The humor of this comes from the combination of *syntactic* and *semantic* ambiguity; the difference between multiple word interpretations, and multiple phrase interpretations.

Colloquial conversations are much more complex than a series of dictionary definitions strung together. When we speak we mean things we don't say, we use sarcasm, implications, negations, and other linguistic tools.

One solution for first understanding sentence structure is use *supervised word alignment*: a person, usually an *undergraduate*, annotates sentences into their grammatical skeleton. From there, the data can be used as a reference in translation and decomposition.

But that isn't enough. Only working on human labor and limited data pool doesn't facilitate accurate and rapid translations. So, while working at Google, DeNero and the translate team scraped the entire internet for every english body of text, mostly from governments and the UN. This resulted in over one trillion words.

The unsupervised data was aligned to the words to infer the skeleton and linking of each sentence and it's translation. What resulted was a series of probabilities. Probabilities which could tell you how often a word was a noun, adjective, or in a clause; as well as how often it translated into other words.

The data guided the reduction of both syntactic and semantic ambiguity through strict probability; similar to how 7th century Arabian scholars [solved](http://en.wikipedia.org/wiki/Frequency_analysis#History_and_usage) the [Cesar cipher](http://en.wikipedia.org/wiki/Caesar_cipher): [frequency analysis](http://en.wikipedia.org/wiki/Frequency_analysis).

### Taking Action

The way many Natural Language Processors are doing in scripting languages, such as Python, which are able to project probability of word definitions, grammatical agents, and implied meaning. This is usually done by deconstructing guided or unguided data into a tree structure.  The [Berkeley Parser](http://tomato.banatao.berkeley.edu:8080/parser/parser.html) is an excellent example of this breakdown.

This is done by comparing each word and its relations to sentence in order to make sense of grammatical structure. For example, "programs must be written for people to read " would would be broken down into its subject,  noun phrases, verb phrases, modifiers, and sub clauses.

![Sentence Structure]({{ "sentence-structure.png" | prepend: site.images_path }})

Parsing sentences in a tree structure makes it extremely easy for computers to navigate and understand the relationship between individual words and the sentence. If you're looking for the hardcore math and code behind actually finalizing a meaning for a sentence, the [Berkeley Natural Language Processing Group](http://nlp.cs.berkeley.edu/index.shtml) of which John DeNero was a member, is an excellent resource. Also, the [Natural Language Toolkit](http://www.nltk.org/book/) explains programmatic implementation for Python.

### Conclusion

Being a linguist helps, no doubt, the the underlying framework for turning human language into machine processable language is still rooted in Computer Science. What DeNero gave a talk on, and currently teaches and studies, is the frontier of converting complex adding machines into speaking/reading human languages.

For the time being, CPUs are only as smart as bugs, but one day, given the proper advancements in computing and artificial intelligence, natural language processing be required, because computers will be able to understand.

