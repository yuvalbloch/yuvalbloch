---
title: "Developing MIRA"
date: 2026-05-21
description: "How we used AI to develop a visualization tool for our research field, and what I learned along the way."
tags: [ai-and-productivity, academic-life]
featured_image: /posts/mira/mira.png 
omit_header_text: true
featured: 3
featured_label: "Building things"
---

Three months ago, my PI Shai Pilosoph offered me a spot on a project he had already started: a new tool for visualizing multilayer ecological networks. I was skeptical. Already on an extension for my thesis, I was afraid to take on anything new when I was already stretched thin. But he showed me what he had built so far, and we talked about how publishing it could support the field in a meaningful way — and add something real to my résumé. So I decided to join, as second author, alongside my colleague Shir who stepped in as the lead writer.

Three months later — none of it anyone's main job — we had a polished, running application called **MIRA** (Multilayer Interactive Rendering Application), deployed at [mira.ecomplab.com](https://mira.ecomplab.com/), and a paper currently in preprint, hopefully soon to appear in _Nature Methods_: [arxiv.org/html/2605.09597v2](https://arxiv.org/html/2605.09597v2).

But as Cavafy wrote: _"Ithaka gave you the marvelous journey."_ This blog has always been about the journey. So here I want to describe my part in developing MIRA — the side quest, not the destination.

<figure> <img src="/posts/mira/mira.png" alt="MIRA application interface" style="max-width:100%; height:auto; display:block; margin: 0 auto; border-radius: 12px;"> <figcaption style="font-size: 0.9em; color: #666; margin-top: 0.8rem; line-height: 1.5; padding: 0 1rem; text-align: center;"> A screenshot of MIRA's features, taken from the paper. </figcaption> </figure>

---

## The Conflict

Like any good story, this one starts with a problem. Otherwise, three busy academics — one PI and two master's students — would probably never have embarked on building an AI-assisted app together.

The challenge is multilayer network visualization. Over the past two decades, multilayer ecological networks have moved from the fringe to the mainstream of ecology. They let us capture the complexity of ecosystems in a way no other framework can. But while the ideas have become more widespread, the number of researchers actually using them remains limited — held back by complex mathematics, unclear definitions, and concepts that are genuinely hard to intuit. That high barrier turns many researchers away before they even begin.

We believed there was a better entry point: if people could _see_ an ecosystem as a multilayer network — really look at it — they could start appreciating its value before tackling the harder theoretical work. But visualization itself is difficult. It requires combining 3D projection with network layout algorithms in non-trivial ways, and the variety of multilayer network types demands a rich feature set to do them justice.

A tool called Arena3D had done this before, but its missing features and unintuitive UI left it as a stepping stone rather than a destination.

So here was the conflict: multilayer networks are vital for understanding and defending ecosystems in an age of rapid change, but without good enough tools, scientists struggle to enter the field.

---

## The Superpower

Enter LLMs — in our case, Claude Code.

All three of us do computational research that requires writing code and implementing complex algorithms. We all use AI in our workflows and had been watching it improve version by version, curious about how far it could go. But in im my individual work, AI assistance had always felt limited. Much of what I do involves designing simulations, where the implementation is only a small part — and the tools and methods I work with are highly niche.

Building MIRA was different. Visualizing multilayer networks combines well-known algorithms: 3D projection, graph layout, UI frameworks. Most of the work is _implementation_, and it draws on a large body of common knowledge — exactly the kind of task where LLMs shine. It also required expertise in app development that none of us had in depth.

We divided the work this way: Shai developed the core application; I used my background in computer science to ensure stability, handle edge cases, and apply good software practices; and Shir led the writing. Together we brainstormed and pitched new features. It worked well. Three months of part-time effort produced a finished app and a paper.

---

## A Revolution Bigger Than AI

Because I have some app development background — however dated — I could see something other might miss: how much the field itself had changed.

Back in 2019, between finishing my military service and beginning my computer science degree, I took a full-stack development course. Even then, a revolution was already in motion. Libraries like React were making app development dramatically easier, which is why courses like mine were multiplying and so many new apps were appearing. What's happened since — modern browsers capable of running complex applications with no backend, better tooling, simpler deployment — is a continuation of that long arc.

<figure> <img src="/posts/mira/iceberg.png" alt="AI as the tip of the iceberg" style="max-width:100%; height:auto; display:block; margin: 0 auto; border-radius: 12px;"> <figcaption style="font-size: 0.9em; color: #666; margin-top: 0.8rem; line-height: 1.5; padding: 0 1rem; text-align: center;"> AI is the visible tip. The iceberg beneath it is a decade of democratized app development. </figcaption> </figure>

When I tell people how easy it has become to build an app, they point to AI. When I look at it, I see AI as the top of a much larger iceberg.

And I call it a revolution for a reason. For the first time, _anyone_ can build an app. As I wrote in [a previous post](https://yuvalbloch.com/blog/the_algorithem_of_the_ring/), many modern apps don't always serve our best interests — they trade in our attention and personal data, and are deliberately designed to be addictive. But now, anyone can build something tailored precisely to their own needs. That could be genuine democratization of the internet. The question is whether people will recognize what they actually need and act on it — or whether this new capability will simply give more power to those who already have it.

---

## What I Learned

**On teamwork:** For the first time in a while, I worked as part of a team. And I discovered that teamwork is like a muscle — if you don't use it, it atrophies. At the start, I was constantly anxious. Every time someone opened a GitHub issue while I wasn't at my computer — and academics work strange hours — I felt an immediate pull to log on. Sometimes I didn't understand a colleague's decision, and it frustrated me. But I learned to trust the process, and my collaborators. By the time I joined the follow-up project (more on that below), I actually _enjoyed_ working as a team.

**On the state of LLMs for coding:** I got a clear view of where things actually stand. And if you know me, you know I tend toward skepticism — I even [wrote about it](https://yuvalbloch.com/blog/ai_and_proudoctivity/). But I have to admit: what Claude Code can do today genuinely exceeded my expectations. It has moved far beyond what was possible even a year ago.

**On side quests:** I learned to appreciate their value. This project refreshed my thinking and let me return to my main work — predicting land use change in underdeveloped tropical countries — with a clearer head.

---

## A Teaser for the Sequel

The good experience of building MIRA left us hungry for more. Shai reached a conclusion: every student in the lab should know how to build small apps to support their own research, so we're never blocked waiting for tools. To put that into practice, he organized a competition. My team built an app called **Figro**. What I learned through _that_ process is the subject of my next post.