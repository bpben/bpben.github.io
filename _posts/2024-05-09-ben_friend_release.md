---
layout: post
title: Ben Needs a Friend tutorial release
author: ben
image: assets/images/20240509.jpg
tags: []
categories: [ LLM, tutorials ]
---

It's ready! In [this repository](https://github.com/bpben/ben_friend) you will find all the materials for my ODSC tutorial "Ben Needs a Friend".

Much of this is adapted from my [LLM App Series]({{site.url}}/categories.html#llm-app-series), but there's a whole bunch of new stuff as well.  All the notebooks are usable with a free Kaggle account (though you will need to authenticate that account!)

The conceit of the tutorial is we're trying to build a "friend" with LLM tools.  Each step builds on the previous one and covers some of the major hot topics in LLM development:

1. Prompt engineering 
2. Fine-tuning
3. RAG
4. Agent workflows

I'm pretty proud of this tutorial.  There are ample deep dives into these topics, but I have struggled to find something that gives a lightweight, accessible demonstration of a suite of them.  I tried to keep things high level, but not abstract things so far that the code can't be repurposed.

One lesson I definitely learned is to do a from-scratch dry run of these tutorials ahead of time.  Kaggle's notebook functionality presented some barriers:

1. You need to have an authenticated account to use notebooks with internet access.  Without internet access, you cannot download the packages you need into the instance.
2. To work with your own version of the notebook, you need to select "Copy+Edit" when viewing the notebook.
3. If 50+ people try to access Kaggle at the same time from the same Wifi, you may have problems :)

Next time - will definitely be running a smaller demo session ahead of time.

Really excited to do more of these.  Welcome any comments and especially any ways you're using these examples in your own work!

