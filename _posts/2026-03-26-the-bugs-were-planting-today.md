---
layout: post
title: The Bugs We’re Planting Today
description: "Some thoughts on using the AI for everything."
category: ai
---

The past few years we’ve been hearing on and on about this idea that basically all of our jobs are going to be replaced by AI. If you work with code, do software engineering, or work in cybersecurity, this will immediately hit.

This might sound a bit too much (albeit I’ve seen it in some posts), but what’s not that extreme is to think that AI is “writing 90% of the code” now. Perhaps not that amount, but AI is here to stay, it is producing a very big part of what devs are pushing, and vibecoding is the new thing in software development.

LLMs work by predicting the next token in a sequence, aka as a probabilistic text generation engine. So, producing text is their speciality, even if the model doesn’t exactly know what he’s producing. They don’t have an understanding of what they’re generating because they don’t think, they were trained the way some people wanted to train them.

On the other hand, AI fatigue is real. Projects like curl shut down their bug bounty program because they were receiving so many AI slop reports that it was impossible to verify them all. Or, open source projects where maintainers are flooded with “extremely low-quality, spammy, and LLM-hallucinated security reports” and PRs and don’t have the time or resources to review them.

And that made me think a bit about the ramifications of all of this. On one hand, you have developers writing correct but not secure code more and more with AI tools, and on the other hand you have entire teams being flooded with slop reports and PRs that’s causing AI fatigue everywhere.

Excluding malicious actors purposefully including a backdoor or vulnerability, at some point, somewhere, some AI generated code will be introduced in production across some private or open source project containing severe vulnerabilities without anyone realizing it. Maybe because no one fully read the PR, or maybe due to AI fatigue reviewing some code changes.

I wonder what examples of these vulnerabilities we’re going to see fail miserably in the following years.

We have plenty examples of bugs and vulnerabilities found years after they were introduced causing enormous damage. In the top of my mind right now I’m thinking of Log4Shell, Dirty Cow, or Shellshock (25 years!).

Unfortunately, I believe that we’re going to see this more and more in the future seeing the current state of development right now.

Are we really 10x more productive and moving faster than ever, or are we just delaying our pain?
