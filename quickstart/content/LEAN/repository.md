---
date: '2026-04-15T09:00:00+03:00'
draft: false
title: 'Repository'
description: 'Explore the LEAN source code on GitHub — understand how the system works, or run your own personalized agent.'
featured_image: '/lean/repository.png'
---

## Open Source

If you are interested in understanding how the system works, or want to run your own LEAN agent with a personalized configuration — focusing on a different country, language, or subject — the full source code is available on GitHub.

[View the LEAN repository on GitHub](https://github.com/yuvalbloch/LEAN)

---

### What the Code Does

The pipeline runs automatically each morning and covers five stages:

1. **Fetch** — pull articles from a curated list of RSS feeds
2. **Deduplicate** — merge stories that share repeated keywords
3. **Filter** — score articles by relevance and significance, drop low-signal items
4. **Summarize** — rewrite each article using an AI model under strict editorial constraints
5. **Deliver** — assemble and send the final HTML digest by email

---

### Stack

- **Language**: Python
- **AI model**: Anthropic (Claude)
- **Delivery**: Buttondown
- **Scheduling**: daily cron job

---

### Run Your Own

The system is designed to be configurable. You can point it at different RSS feeds, adjust the filtering rules, and run it on any topic or region — not just Israel. Instructions for setup are in the repository README.
