---
title: "Three Years, Six Semesters: What Writing My Thesis Actually Taught Me"
date: 2026-08-13
description: My Master’s research was the center of my world for three years. Now that it's over, I look back and ask what I really learned in the process—not about modeling, but about life and work.
featured_image: /posts/images.jpeg
tags: [academic-life]
omit_header_text: true
draft: false
featured: 4
featured_label: "Reflection"
---

Today I submitted my thesis. It's the kind of milestone that should feel like a finish line, but it doesn't quite — I still have to defend it, and I'm in the middle of submitting a paper drawn from it to _Nature Communications Earth & Environment_. Still, by the time that review process wraps up, in this journal or another, I'll likely already be somewhere else in my life. So this feels like the right moment to look back at the continuous stretch of work that's ending today, even if fragments of it will follow me a while longer.

The whole thing took three years, or six semesters if you don't count summers. What surprises me looking back is that each semester taught me something completely different — not about ecology or modeling specifically, but about how to actually do the work of research.

## Autumn 2023 — Working When the World Falls Apart

I arrived in Be'er Sheva in late August, signing my apartment lease the same day the lab I was joining kicked off with a conference. I brought light equipment, slept there for the duration of the conference, then went back to Mitzpe Ramon to collect the rest of my belongings. I still had one exam and a project submission left to finish my undergraduate degree, so everything happened in a rush.

Then the war broke out.

I was expecting to be called up — I'd served as an auto-electrician — but in the end the army didn't need me. What followed was a strange kind of limbo: I started working, but never on stable footing, since I could be summoned any day. The university was nearly empty. The semester hadn't officially opened because many students, including several labmates, had been enlisted, and many who hadn't left the city anyway, since Be'er Sheva sat uncomfortably close to the front.

Walking into an almost-empty campus while sirens rose and the news kept getting worse felt disorienting. It took me a while to understand what I actually needed from the work. It wasn't just a distraction. In the face of real cruelty, having the chance to try to build something for the benefit of people felt like a genuine privilege. Eventually students trickled back, the semester opened, and I worked quickly through the courses I needed to make the jump from computer science to ecology.

## Spring 2024 — Keep It Simple

By the end of that first semester, I knew what I wanted to research. My lab was part of a collaborative project in Madagascar, studying land use and the disease risks it created for local communities. I decided to build a model connecting land-use change to tick populations — first [a tick population model](https://yuvalbloch.com/research/tick-population-model/) suited to a tropical landscape, then coupled with cellular automata to capture spatial change.

It turned out to be a genuinely hard problem, mostly because the existing models had all been built for temperate, cool-climate systems. I started sketching equations and testing them in small Jupyter notebooks, watching how the dynamics behaved. But with each iteration, the model grew — three differential equations became twelve. Eventually I realized my instinct to force a metacommunity framework onto a system that wasn't clearly a metacommunity was the wrong move. The bigger lesson was more general: the question isn't whether a factor is technically relevant to your model, it's whether the model still holds value without it. If it does, drop it.

## Autumn 2024 — Commit to Your Idea

This is when things got both exciting and frightening. By early autumn I finally had a version of the model behaving the way I wanted, which meant switching gears entirely. I'd been writing small, disposable notebooks to test one idea at a time. Now I had to build a real code repository — one that would carry me through the rest of the thesis. Suddenly, decisions about variable names and database structure had consequences that would outlast the semester. It was strange to keep working on one model while it quietly grew from hundreds of lines of code to thousands, and eventually tens of thousands, while acting like I knew what I was doing when, honestly, I never fully did.

By spring the model was solid, with results that mattered — sensitivity analysis showed it responded meaningfully to the kinds of land-use changes we'd expect across the tropics. Given how far the work had expanded, my advisor Shai and I had our first real conversation about scope. I started thinking the tick model alone could be a full thesis, maybe even a small paper on its own. my PI encouraged me to push further — something he'd keep doing, in other decsions. I still don't know whether that was the right call. I learned a great deal and built a real understanding of modeling, but I also didn't finish on the timeline I'd planned. What I do know is that I arrived at that decision the wrong way: through a string of small choices and repeated conversations, rather than sitting down early and aligning expectations from the start.

## Spring 2025 — Care for Your Students

My first TA position, in spring 2024, was light — one hour a week, three students. This time it was Python for biology students: two-hour sessions, four different groups, so many students that by the end of the semester I still couldn't remember all their names. I hadn't planned to take on this much, but there wasn't really a choice. my PI advice was that only my research mattered for my academic future, so I should spend minimal effort elsewhere, and I tried, at first, to follow that.

But Python is genuinely hard for a lot of biology students. Some are afraid of programming outright, some find it deeply counterintuitive, some just struggle. Despite wanting to protect my research time, I ended up pouring most of that semester into teaching. It probably won't add much to my CV, but it was one of the most satisfying jobs I've ever had — knowing that for at least some of those students, I helped move programming from something strange and frightening into something they could actually do.

## Autumn 2025 — Keep Your Focus

The summer of 2025 brought two hard things at once: the round of war between Israel and Iran, and my grandfather's death. I was emotionally worn down, and I found myself retreating into mindless videos on my phone, which quietly wrecked my attention span. I started offloading work to AI tools not because it was the right approach, but because focusing on anything myself had become difficult — sometimes retrying the same task with AI over and over when that wasn't even the right way to solve it.

A trip to Greece made the pattern obvious to me. I started limiting my phone use, added a lot more physical activity, took a short work retreat in Mitzpe Ramon, and got more deliberate about which tasks I could hand to AI tools and, just as importantly, which ones I couldn't.

That semester I also started writing seriously, and the writing itself reshaped the story of my research — it shifted from being primarily about ticks to being about land-use modeling and its connection to real-world problems. By the end of the semester, it was clear I needed one more to turn all of it into both a thesis and, more importantly, a paper that actually communicated what I'd found.

## Spring 2026 — Know When to Stop

This is the hardest part. Research never really ends — there's always another angle, another test, another improvement, [as one more reproducibility bug hunt proved right up to the very end](https://yuvalbloch.com/research/making-reproducible-science/). At some point you have to decide it's enough.

I decided early on not to pursue a PhD in the same lab. I care about this research area, but I went into it knowing very little about what doing research actually meant. Maybe I'll come back to it someday. But now that I understand the process better, I want to look forward and ask what I actually want to study next — and to do that, I need to leave this project behind me.

So: decide it's enough. Submit the thesis. Submit the paper, and if it isn't accepted, send it somewhere else it might end for best or worst but anyway I keep moving forward.