---
layout: page
title: The Clacks
description: Subscribe to authors and articles on the arxiv (& biorxiv) - coming soon
category: fun
---

I've been annoyed by the huge amount of irrelevant new papers on the arxiv for a while now.
While Google Scholar helps keeping track of anyone who bothered setting up an account, I'm not quite happy with the alert system (in particular the fact that everything goes directly into my email inbox).

Things got several orders of magnitude worse when I started switching my focus towards computer science and biology.

So, here's the idea: I want to be able to go to a website, where I get notified whenever an author I've added to a subscription list puts out a new article. 
Also, I'd like to be notified whenever an important article gets cited by some new work.

I've scrambled up a flask app that does the first thing (for arxiv and biorxiv) and a very rudimentary version of the second (using openalex). 
It runs on my machine.
Happy to share if anyone is interested, but too ashamed to put it out there.

Here's how today's notification looks like.

![clacks screenshot](/assets/img/clacks-prototype.png){: width="900"}