---
title: Three lessons on Bayesian optimization, and one on humility
featured_image: /research/bysian.png
date: 2026-07-17
description: How a failed reproducibility test exposed three convergence bugs in my Bayesian optimization — stochastic simulations, unidentifiable parameters, and the wrong scale — and one lesson in humility I get in the way.
draft: false
omit_header_text: true
---




Two weeks ago, I told my advisor that my thesis was ready. We decided to delay the submission a little — partly so he could find a referee, and partly so I could keep my scholarship while I converted the thesis into a paper and made sure my code was reproducible.

Three days ago, I finished building a simple pipeline that would let future researchers reproduce all of my results without needing me around. I ran a quick test to confirm that I could reproduce everything without diving back into the code myself — and when I ran a full reproduction through the pipeline, I got completely different results.

Over the next three days I tracked down what was causing this massive stochasticity. I still plan to run a few more tests before I edit the thesis, but I'm fairly confident things are fine now. So I want to share the lessons I learned along the way.

This post has two jobs. By documenting the problems I ran into, I hope to help others avoid them. But maybe the most important lesson was about humility — because, looking back, my mistakes were a little trivial.

In _Outliers_, Malcolm Gladwell popularized the idea that you need 10,000 hours of practice to achieve true mastery of a craft. My master's stretched to three years, but during that time I also worked as a TA, took classes, and did plenty of other things that weren't research or modeling. I've probably spent no more than 2,000 hours actually practicing research and scientific modeling. It was a useful thing to remember: I'll have my master's degree soon, but I'm still a long way from real mastery of the craft.

## The problem: Bayesian optimization convergence

My research uses a cellular automata–Markov (CA-Markov) model to simulate dynamic land use — specifically shifting cultivation — which is a fairly niche topic. But the problem I ran into is a common one: parameter optimization convergence.

In a stochastic cellular automaton — a tool that dynamically changes the state of each cell according to probabilities defined by the cell's state — the weight I give to the neighborhood effect matters enormously. It controls the model's behavior across a whole spectrum: high weights produce geometric patterns like spirals, while low weights produce an almost completely random mix.

To fit this parameter, I used Bayesian optimization, choosing parameters so that the model would generate landscapes whose configuration indices resembled those of the land-classification map. Running the optimization a few times, I got what I considered fairly similar results in how the maps looked and behaved — and I didn't pay much attention to the fact that the underlying parameters were quite different from run to run.

It was only when one run produced a better fitness than any I'd seen before — yet with entirely different parameters, _and_ an entirely different model output — that I realized I had never actually confirmed the Bayesian optimization was converging.

### Background

Here's a very basic explanation of the model that uses these parameters. In my system, the main driver of land-use change is shifting cultivation: land at different levels of recovery can turn into a shifting-cultivation plot, which can then degrade into bare land, which slowly recovers back up through the recovery levels. For each transition there is a _transition demand_ that specifies how many cells of each type change into each other type. To choose the specific cells that actually change, I score each candidate cell with the formula

$$\text{score} = 1 + \alpha_{i,j}, NW$$

where $NW$ is the count of neighboring cells that support the transition and $\alpha_{i,j}$ is the neighborhood weight. I then use weighted random sampling over these scores to pick the cells that undergo the transition.

I ran into three problems that undermined the optimizer's ability to converge.

### 1. Stochasticity in the simulation

The first was the stochasticity in the simulation itself. On each round, the optimizer would choose a promising parameter set, run the simulation, and compute the fitness function on the resulting map. But that map wasn't determined by the parameters alone — the simulation makes many stochastic choices along the way, so the same parameters could yield very different maps.

To address this, I went back to my fitness function and tested its signal-to-noise ratio. That told me which fitness functions best captured the real, process-driven differences behind each parameter set, rather than random noise. I also combined the Bayesian optimization with repetition: for each parameter set, the optimizer now runs the simulation several times and uses the average fitness instead of a single noisy run.

### 2. The parameter space

My model has seven transitions: from various natural land types into shifting cultivation, from shifting cultivation into degraded land, and across the recovery gradient. Trying to fit seven parameters against only a handful of configuration indices created an _identifiability_ problem. It wasn't that the optimization failed to find the right solution — it was that a whole region of parameter space had almost the same fitness. Many different solutions were all equally good.

Think of minimizing the fitness function $\min |x + y - 6|$. It has infinitely many optimal solutions: $(3, 3)$, $(2, 4)$, $(-100, 106)$, and so on.

The fix was to stop thinking in terms of transitions and start thinking in terms of _processes_. Instead of fitting a different $\alpha$ to each transition — secondary forest → shifting cultivation, and so on — I now fit one $\alpha$ per process (for example, cultivation, or degradation) and apply it to every transition of that type.

This not only made my solution well-defined without lowering the final fitness — it also made the results far easier to interpret.

### 3. The scale of the parameter

As soon as I started experimenting, I noticed that $\alpha$ could take on a huge range of values — from 1 to 10,000 — and that its effect shrinks as the value grows. So from the start I chose to fit it on a log scale (an idea I was quite proud of) — only to discover that a log scale doesn't actually make sense. $\alpha$ doesn't affect the system on a logarithmic scale, but on a _reciprocal_ one.

Let me define $\alpha'$ as the ratio between the sampling weight of a cell with no neighborhood contribution ($NW = 0$) and one with a unit neighborhood contribution ($NW = 1$):

$$ \alpha' = \frac{w(NW=0)}{w(NW=1)} = \frac{1}{1+\alpha}. $$

Optimizing $\alpha'$ instead of $\log(\alpha)$ gives a clean, bounded domain:

$$ \alpha' \in [0, 1], $$

and, more importantly, it gives the right amount of attention to different parts of the range. Half of the optimization domain now corresponds to $\alpha \in [0, 1]$:

$$ \alpha' \in \left[\tfrac{1}{2}, 1\right] \quad\Longleftrightarrow\quad \alpha \in [0, 1], $$

while the enormous range $\alpha \in [100, 10000]$ collapses to a tiny sliver:

$$ \alpha' \in [0.0001, 0.01] \quad\Longleftrightarrow\quad \alpha \in [100, 10000]. $$

And, most importantly, it lets me report a genuinely meaningful parameter in my paper.

## The illusion of the trivial solution

So why didn't I think of all this earlier? Given what I know about my model and about parameter optimization, some of these decisions — especially the last one — look trivial in hindsight.

But I think that while this was a lesson in humility, it also taught me something else: the solution to a riddle always looks trivial once you have it. The truth is that each of these fixes required a clear view of my system, a clear view of Bayesian optimization, and — most importantly — the ability to spot a needle in a haystack. There are millions of potential problems in complex ecological modeling, and when we try to work out what went wrong, we're searching an almost infinite space. I caught this one by accident. But I believe that true mastery of scientific modeling is being able to see these things coming in advance.