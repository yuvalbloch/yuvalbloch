---
date: '2026-11-21'
draft: false
title: 'ESP32 Compatibility Table'
weight: 2
number: '02'
role: 'Project #1'
icon: 'chip'
status: 'In progress'
description: 'Which community libraries still compile on the new ESP32 Arduino core? A public table built from real compile logs, plus a tool that tells you what to pin.'
---

## The problem

A new major version of the ESP32 Arduino core (4.0) was released on 19 November 2026. Nobody knows yet which of the thousands of community libraries — for sensors, displays, networking, LEDs and motors — still work with it.

Last time this happened, moving from 2.x to 3.x in 2024, many libraries broke. It took the community months of scattered forum posts and GitHub issues to work out what still worked. Version 4.0 is built on ESP-IDF 6, which removed legacy drivers, treats compiler warnings as errors and changed the crypto API, so a similar wave of breakage is likely. Espressif officially tests about 10 libraries. Everything else is untested.

### The pieces

- **ESP32** is a family of cheap Espressif microcontrollers with built-in Wi-Fi (and usually Bluetooth). It is the default choice for hobby and small-product IoT.
- **The ESP32 Arduino core** lets you program these chips in the simple Arduino style. Under the hood it runs on Espressif's native framework, ESP-IDF.
- **Libraries** sit on top of the core, and some reach directly into ESP-IDF. Libraries that use only plain C++ or Arduino functions usually survive an upgrade. Libraries that drive timers, PWM, LEDs or fast display interfaces directly usually break.

## The solution

Compile the most popular libraries against each core version and chip, and publish the results as a table — together with a small tool that tells you which library versions to pin for your project.

- **Libraries:** the most popular ESP32-compatible libraries, starting with the top 50 and growing to 500.
- **Library versions:** the latest release plus the last 2–3.
- **Core versions:** 2.0.17, the latest 3.0.x, 3.3.12 and 4.0.0.
- **Chips:** ESP32, ESP32-S3 and ESP32-C3 first — covering both CPU families, Xtensa and RISC-V.
- **The test:** compiling 1–2 of each library's own example sketches.

### Each result is a fact that never expires

Every result is tied to an exact library version, core version and chip. When a maintainer fixes a library, the fix shows up as a new row; the old row stays true. A daily job compiles only new releases, and each new core version simply adds a column.

## Why this one first

Blindspot surfaced it, and it has the best mix of timing, reach and effort right now:

1. **The timing is right.** The new core was released days ago. If the table comes first, it can become the table everyone uses.
2. **It holds up against AI.** The value is in results that only exist after actually compiling. An assistant can't guess them, and a copycat has to redo the work.
3. **It is small.** Most of the work is setting up a compile farm and letting it run.
4. **The value for effort is very high.** Thousands of ESP32 developers need this, and nobody has it.

## The AI workflow experiment

Each Wild West project also tests a different way of working with AI. This one is the most AI-driven: **the AI plans and builds, and I act as the approver.** I don't write code and do as little planning as I can; the AI explains each decision it needs from me in plain language, as it would to a non-technical manager.

| Task | AI | Me |
|---|---|---|
| Planning | Writes every plan: phases, design, task lists | Approves or asks for changes |
| Code | Writes all of it: compile runner, scheduler, website, pinning tool | Reviews the results, not the code |
| Running the farm | Writes the jobs and fixes them when they break | Starts runs, watches costs |
| Failure triage | Groups compile errors and labels the root cause | Spot-checks the biggest groups |
| Publishing | Builds the site and release notes | Decides what goes public and when |

> **The one rule the AI cannot bend:** every ✅ or ❌ in the table must come from a real compile log. The AI may write the tools, group the errors and explain them, but it never decides pass or fail by itself. That is what makes the table trustworthy.

I'll be measuring the hours I spent against the hours it would take by hand, how many plans I approved as written, where the AI got stuck or was confidently wrong, and whether the table holds up once other people use it.

## Status

Under construction. The table will be published here on this website.
