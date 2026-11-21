---
date: '2026-11-21'
draft: false
title: 'Blindspot'
weight: 1
number: '01'
role: 'The scout'
icon: 'compass'
status: 'Active'
description: 'Mines public online communities for the questions people keep asking, and returns a ranked shortlist of problems worth solving.'
---

## What it does

Blindspot is the scout of the Wild West project. You give it a broad subject — say, *home caregiving* or *ESP32 development* — and it mines public online communities for the questions people keep asking. It returns a ranked shortlist of **recurring problems**, each graded on how worthwhile it would be to build a tool for it.

The point is to choose problems by what people are actively asking for, not by what I happen to find interesting.

## How a problem is graded

Each problem gets four separate grades:

| Grade | Question it answers |
|---|---|
| **Value** | How many different people ask about this, and across how many communities? |
| **Gap** | Is there already a good solution, or is the space still open? |
| **Timing** | Is this problem growing, peaking, or already solved? |
| **Effort** | How many working days would it take to build a tool for it? |

They are combined into a single opportunity score:

```
V = ln(1 + A + 0.1·M) · D/(D+2)        A = distinct askers
S = V · (0.5 + G) · (0.5 + T) / E      M = silent "me too" signals
                                       D = effective number of communities
```

Value grows with the number of distinct people asking, not with the number of posts, and is discounted when all the noise comes from a single community. Effort is estimated in working days: for each problem, Blindspot proposes a tool and breaks building it into 3–7 steps with days per step.

## The pipeline

| Stage | What happens | LLM? |
|---|---|---|
| **Suggest** | A small model proposes where to look: Stack Exchange sites and tags, Hacker News queries, Discourse forums. Each source is validated before use. | 1 cheap call |
| **Collect** | Pulls the last 24 months of posts (up to 20k) from Stack Exchange, Hacker News and Discourse. | No |
| **Extract** | Finds the problem sentences: "is there a tool for…", "how do I…", and their close relatives. | No |
| **Tree** | Embeds every problem locally and clusters them into a hierarchy of problem families, from broad themes down to specific complaints. | No |
| **Label** | Names each family from its most representative posts. | Small model |
| **Grade** | Grades the top families using free evidence from GitHub, npm, Semantic Scholar and existing answers. | ≤10 calls |

Most of the work runs locally and costs nothing; the language model is used only where judgment is needed. Authors are stored only as hashed IDs, and every post keeps its source link for attribution.

A web dashboard lets me explore all the results, re-weight the grades, filter by date, and mark each problem as keep, maybe or drop.

## What the first runs taught me

I ran Blindspot on eleven test subjects and then checked the best ideas against existing competition. A few lessons stood out.

### Problems appear when something changes

The strongest opportunities show up when people suddenly need their work to function in a situation it wasn't built for:

- **A big program updates and its ecosystem lags behind** — QGIS 4, Blender 5, KiCad 11, the ESP32 core.
- **A product becomes expensive or closed** and people move to free alternatives.
- **A platform reaches end of life** and everyone has to migrate.

These are short-lived opportunities. The change lands, things break, and within weeks either tools appear or people fix things by hand and move on.

### The best problems live where software meets hardware

Of the five ideas that survived the competition check, four touch physical devices. A programmer with an AI assistant cannot vibe-code a solution without the hardware in front of them, so fewer people attack these problems. Yet the hardware is cheap — a few dollars for an ESP32 board, about $100 for a small smart-home lab.

### What kind of tool survives

| Holds up | Gets cloned fast |
|---|---|
| **Datasets built by running things** — results nobody has until they actually compile or test everything | Static linters and code converters |
| **Joining scattered data per project** | "Doctor" tools that read your logs |
| **Live probes of the user's own environment** | Config generators |

The test for any idea: *what does my tool know or see that a chat assistant can't?*

### Common traps

- **The vendor will ship it.** The company that caused the breaking change has the strongest reason to ship the migration tool. Aim at what they won't build.
- **Arriving after the deadline.** Most waves Blindspot found had passed by the time it proposed a tool.
- **Few GitHub stars doesn't mean an empty niche.** GitHub is now full of small AI-built tools, often several per niche.

### Relevant problems disappear fast

This is the Wild West hypothesis in action: problems appear quickly after a change, but solutions do too. For one migration deadline, three separate testing tools appeared within a few months. For one major software release, two paid scanners appeared within weeks.

So the next version of Blindspot will:

1. **Watch announcements, roadmaps and end-of-life calendars**, not just complaints — the best time to catch a change is between its announcement and its arrival.
2. **Search for competitors deeply and recently**, including marketplaces, vendor release notes and repositories created in the last 90 days.
3. **Favor speed over polish.** A small tool shipped before the change lands beats a better one shipped after.

## Status

Blindspot is working and in active use — it picked the first Wild West project, the [ESP32 compatibility table](/wild-west/esp32-compatibility-table/). The source code will be published on [GitHub](https://github.com/yuvalbloch).
