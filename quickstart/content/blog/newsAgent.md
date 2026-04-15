---
draft: false
date: 2026-04-12
title: How and Why I Built My News AI Agent
description: I built an AI agent to read the news the way I did fifteen years ago — once a day, with focus, and then closing it. Here's how and why.
featured_image: /images/robodog.png
omit_header_text: true
---

I fell for the trend. I built my own AI agent — and worse, I vibe-coded it. I suppose even I eventually surrendered to the spirit of the era. But I did so with a specific goal: to use modern tools to return to something older. To the era of print.

## Moving Forward by Reaching Back

Let me describe how I consumed news fifteen years ago, when I was still a high school student. Every afternoon, after coming home, I'd pick up the newspaper and spend about forty minutes reading what had happened in the world. I'd focus, try to understand the context of events, read what interested me — and then close it and go do homework, hang out with friends, or read a book.

When I was seventeen, I got my first smartphone. At first, the experience wasn't so different from print. If you opened a news app at a random hour, there was a clear hierarchy: a lead headline, a few secondary stories, maybe some opinion. The only real novelty was breaking news — events unfolding in something close to real time.

But gradually, the logic of breaking news colonized everything. Headlines started changing every hour. The order of articles shifted constantly. Videos crept in. After a decade of this drift, opening a news app no longer gave me a clear summary of what had happened. It gave me an experience designed to keep me in a state of constant agitation — a hunger for more information that never resolved into better understanding.

This is what Derek Thompson means when he writes that all media has converged on television's prime directive: never let the viewer look away. It's not a stream of information trying to create a coherent picture. It's a stream of information that replaces coherence with engagement.

So I wanted to go back. To have one or two good summaries a day — something that highlighted what mattered and let me seek out more if I chose. My first instinct was to simply start reading a print newspaper again. But a few things about the new world were genuinely better, and I didn't want to give them up:

- **Sustainability and cost** — print requires real resources, from me and from the planet.
- **Multiple perspectives** — even the best newspaper has a tilt. Comparing viewpoints is hard in print, where you'd need to buy several different papers.

There was also something print never solved: the writing style. News writing has become increasingly emotional — and that clutters the information as much as the format does. This happens in print as much as it does online.

So I designed my own AI agent to solve this for me. But before I explain what it does, let me explain what an AI agent actually is.

## What Is an AI Agent?

The core of the AI revolution of the last few years is the large language model, or LLM. These models do one thing well: they take text as input and produce text as output. But not every task can be handled by a single send-and-receive exchange. An "agent" is a program that does something useful in the world — and along the way, calls an LLM one or more times as part of that process.

## How It Works

First, I defined the subjects I care about and roughly how much space each should get.

The pipeline runs like this:

1. The program downloads RSS feeds from several news websites. (RSS is a format that lets software read news in a structured way.)
2. It does an initial deduplication pass based on repeated keywords, to remove multiple articles covering the same story.
3. It passes each remaining article to an LLM, which decides whether it meets my standards of relevance and significance.
4. The articles that pass are collected into a single block of text, which becomes the context for the next LLM call.
5. A second LLM call uses that context alongside a system prompt that instructs the model on tone, structure, and priorities.
6. The LLM returns HTML. The program wraps it in a header and footer I wrote — a brief text I designed to put me in the right frame of mind for the serious activity of reading the news.
7. The result is sent to me by email.
8. This whole process runs on a schedule, twice a day: 6:45 in the morning and 6:00 in the evening.

## Future Development

Below you'll find an example digest (text only, without the HTML wrapper). You'll notice it has some rough edges — it leans heavily on The Times of Israel, and the science section doesn't always surface the most important stories. I still need to refine the prompts. I also want to make it easier to adjust the prompt, the filtering logic, and the RSS feed list through some kind of simple dashboard, without touching the code directly.

You might also notice that the digest is a little boring. That's not a bug — it's the point. The news should be boring. I'm reading to understand what happened in the world, not to be pulled into a rabbit hole.

One feature I'm considering for the future is a crisis alert: a separate process that runs more frequently but only sends an email if something genuinely significant occurs. The tricky part is calibrating the threshold — too loose, and it just becomes inbox clutter all over again.

---

## Example Feed

_Your morning digest_

# Sunday, April 12

Good morning, Yuval.

You are about to read a summary of the current state of the world.

> Remember: The facts of the world do not change based on whether you like them or not. Your beliefs matter only through the actions you take.
> 
> Approach this with a beginner's mind — aim for clarity, not certainty.
> 
> You do not need to know every detail. Understand enough to see the bigger picture, so you can make better decisions and contribute in a meaningful way.

### Israel

Prime Minister Netanyahu stated that Israel's campaign against Iran is "not over" while citing what he described as historic achievements. Opposition leaders responded that the war's goals remain unfulfilled, with one noting that "when you win, you don't need to declare it every few days."

_Source: The Times of Israel_

The IDF reported striking over 200 targets in Lebanon over the past day, with two Israeli soldiers wounded in combat in south Lebanon. Lebanese sources reported 10 people killed in the strikes. Israel and Lebanon are preparing for direct negotiations, though Hezbollah has criticized the planned talks.

_Source: The Times of Israel_

Israeli leaders responded to reports that Turkey is seeking to jail them by criticizing Turkish President Erdogan. Netanyahu accused Erdogan of accommodating Iranian-backed groups, while other ministers issued statements condemning Turkish policy toward Kurds.

_Source: The Times of Israel_

The IDF conducted strikes in Gaza that Palestinian sources say killed several people. The military stated it targeted operatives planning attacks against troops. Separately, an Israeli soldier was seriously injured in an operational accident and hospitalized.

_Source: The Times of Israel_

Syrian authorities announced the arrest of five individuals allegedly connected to a Hezbollah-linked plot to kill a rabbi in Damascus. The suspects reportedly attempted to plant a bomb near the target's home. Syrian officials stated the arrests demonstrate protection of the Jewish community.

_Source: The Times of Israel_

### World

US-Iran direct talks in Pakistan concluded after 21 hours without reaching an agreement. Vice President Vance stated that Iranian negotiators refused to disavow a nuclear program that could enable weapons development. Iran cited disagreements over control of the Strait of Hormuz as another point of contention.

_Source: The Times of Israel_

Hungarians voted in an election that could end Prime Minister Viktor Orbán's 16-year rule. Most polls show challenger Péter Magyar, who leads a grassroots party, ahead of Orbán, though the outcome remains uncertain. The election is being watched by officials in the EU, Russia, the US, and Israel.

_Source: BBC News, The Times of Israel_

Germany's far-right Alternative for Germany party adopted what observers describe as a more radical manifesto ahead of upcoming elections. The party currently leads opinion polls in the eastern state of Saxony-Anhalt.

_Source: BBC News_

### Science & Economy

Scientists have confirmed a 67-year-old theory about vitamin B1's function in the body by stabilizing a highly reactive molecule in water. The research team achieved what was previously considered extremely difficult, and the findings may have applications for developing greener chemical manufacturing processes.

_Source: ScienceDaily_

Researchers discovered that loss of smell may indicate Alzheimer's disease years before cognitive symptoms appear. The study found that immune cells in the brain destroy smell-related nerve fibers after detecting abnormal signals, with this damage occurring in early disease stages. The finding could enable earlier identification of at-risk patients.

_Source: ScienceDaily_

### Good News

The Artemis crew returned safely to Earth after completing a nine-day mission to the Moon. The four astronauts splashed down in the Pacific Ocean, having traveled further from Earth than any humans in history.

_Source: BBC News_

Syrian authorities successfully prevented an attempted attack on a rabbi in Damascus, arresting five suspects before they could carry out their plan. Officials stated the operation demonstrates ongoing protection of religious minorities in Syria.

_Source: The Times of Israel_

---

_Today's deep dive · ~15 min read · appeared in 5 sources_

### US-Iran Direct Talks in Pakistan

**Abstract**

The United States and Iran held their first direct negotiations in years, meeting in Pakistan for over 21 hours before talks concluded without an agreement. The discussions centered on Iran's nuclear program and control of the Strait of Hormuz, with both sides maintaining their core positions. The outcome leaves open questions about the future of US-Iran relations and regional stability in the Persian Gulf.

**Background**

US-Iran relations have been characterized by tension and limited diplomatic contact for decades. The two countries have not had formal diplomatic relations since 1980, and negotiations have typically occurred through intermediaries or in multilateral formats. Recent military actions, including Israeli and US strikes on Iranian nuclear facilities and Iran's mining of the Strait of Hormuz, created both pressure and potential openings for direct engagement.

The Strait of Hormuz represents one of the world's most significant maritime chokepoints, with approximately one-fifth of global oil supplies passing through its waters. Control over the strait has been a persistent source of tension, with Iran historically claiming the right to regulate traffic while the US maintains freedom of navigation principles.

**What happened**

US and Iranian negotiators met in Pakistan, with talks extending through the night for more than 21 hours. Iran reportedly demanded control over the Strait of Hormuz and a truce in Lebanon as conditions for any agreement. Vice President Vance led the US delegation and stated afterward that Iranian representatives refused to disavow nuclear weapons capability.

During the negotiations, President Trump stated publicly that it made "no difference" to him whether a deal was reached, claiming the US had already won "regardless" of the outcome. The US military announced that Navy destroyers are working to clear mines from the Strait of Hormuz, with additional forces expected in coming days. Iranian media disputed Trump's claims about the destruction of Iranian mining vessels.

**Perspective A:** The talks represent a diplomatic opening after a period of military escalation. Even without an immediate agreement, direct communication between US and Iranian officials could reduce the risk of miscalculation and establish channels for future negotiations. The fact that both sides engaged for 21 hours suggests some willingness to find common ground.

**Perspective B:** The failure to reach any agreement, combined with both sides' public statements maintaining their positions, suggests the talks may have been more about domestic political messaging than genuine negotiation. The ongoing US military operations to clear the strait and Trump's dismissive comments about the need for a deal indicate that the US may be pursuing a pressure strategy rather than seeking compromise.

---

_You have finished reading your summary of the world._

_Now step away, focus on what matters, and do your part to make it better._