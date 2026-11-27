---
date: '2026-11-27'
draft: false
title: 'Bioconda on Apple Silicon'
weight: 4
number: '03'
role: 'Project #2'
icon: 'dna'
status: 'Live'
description: 'Which bioinformatics tools really install on Apple Silicon Macs before Rosetta goes away? A nightly table built from real solver runs, checked against real installs on real machines.'
---

## The problem

Most bioinformatics software is installed with **conda**, from a channel called **bioconda** (about 13,000 tools: aligners, assemblers, quality control, statistics). Each tool has to be built separately for each kind of computer.

Apple Silicon Macs (M1–M4) can run tools built for older Intel Macs through a translator called **Rosetta 2**, and many labs do this without knowing it. That door is closing: **macOS 27 is the last macOS with full Rosetta 2**, and macOS 28 (autumn 2027) keeps only a small part of it, for games. Intel-only tools will stop working on Macs.

In bioconda, Apple Silicon builds are **opt-in per tool**: someone has to ask for them. Many never did, and nobody publishes which tools are affected. The same is true for arm64 Linux (cloud servers such as AWS Graviton).

## The solution

A public table, updated every night, that answers for each tool: **does it install natively on Apple Silicon and on arm64 Linux, at which versions, and what should I pin instead?**

- **What's tested:** the 1,000 most-downloaded bioconda tools plus every tool used by the two big pipeline collections, nf-core and Snakemake: about 1,700 tools, each at its newest version and the 3 before it. Plus all 2,580 nf-core and Snakemake pipeline steps, exactly as their authors wrote them.
- **How:** a real conda solver checks every tool on 4 kinds of computer, about 31,000 checks a night on 8 cloud machines in about 10 minutes.
- **Checked against reality:** 102 cases were also installed for real on Apple Silicon and arm64 Linux machines, and **204 of 204 matched** the table. Every week, the 300 most-used tools are installed for real and run their own built-in test.

**First findings:** 1,359 of 1,702 tools install on Apple Silicon, but **227 popular tools work on an Intel Mac and not on Apple Silicon**, and **482 of 2,580 pipeline steps** will stop working when Rosetta goes. In most cases the cause isn't technical: the tool's recipe simply never asked for an Apple Silicon build.

## Why this one

1. **There's a deadline.** Rosetta goes away in autumn 2027. A list that exists before then is useful; one that comes after is a post-mortem.
2. **It's the second data point for the experiment.** Before building, I tested whether a general AI coding agent could just answer the question. It could, for one lab's setup, in about 35–50 minutes. So a one-off checker wasn't worth building. What an agent can't easily do is the scale (thousands of tools, every night), the history ("the Apple Silicon build disappeared on 3 December"), the real machines, and being there before you ask. This project tests whether a public table still wins when an AI agent could answer the question on demand.

## The AI workflow experiment

Like the ESP32 table, this one is **AI-driven: the AI plans and builds, and I approve**, but with fewer check-ins. I approved the plan once, and after that the AI asks me only at three gates: the calibration report, the live page before launch, and the posts before they go out.

> **The one rule the AI cannot bend:** every ✓ or ✗ comes from a real solver run or a real install log, stored with the exact command and date. The AI writes the tools but never decides a result, and every result links to its log.

**Where the AI was confidently wrong** (part of what I measure): its first two runs of the weekly real-machine test had bugs in its own test runner, which marked every tool "no test", then "test failed". It caught both within the hour, removed those results, and listed both corrections publicly in the methodology.

## Status

**[Open the live table →](/wild-west/bioconda-arm/)** Updated every night. The code, every result and every log are public on [GitHub](https://github.com/yuvalbloch/bioconda-arm-readiness).
