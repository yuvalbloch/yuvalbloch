---
lang: "en"
title: 'Publications & Output'
date: '2026-08-16'
draft: false
description: "Papers, preprints, thesis, software, and conference output by Yuval Bloch — computational ecology, land-use modelling, and multilayer network visualization."
omit_header_text: true
---

## Publications & Output

Papers, software, and research output from my M.Sc. in the *Ecological Complexity Lab* at
Ben-Gurion University of the Negev, working with Prof. Shai Pilosof.

---

### Papers & preprints

**Nehoray, S. M., Bloch, Y., & Pilosof, S.** (2026). *Interactively visualizing biological
multilayer networks using MiRA.* arXiv:2605.09597 \[cs.SI\].
<span class="yb-links">[preprint](https://arxiv.org/abs/2605.09597) · [live application](https://mira.ecomplab.com/) · [how it was built](/blog/mira/)</span>

A browser-based, installation-free web application for visualizing biological multilayer
networks, with seven complementary visualization modes. I contributed to the application's
stability, edge-case handling, and software practices, and to feature design.

**Bloch, Y., & Pilosof, S.** *A multiscale cellular automata–Markov framework for modelling
shifting cultivation and agroforestry landscapes.* Manuscript in review.
<span class="yb-links">[code](https://github.com/MadagascarEEID/LUC_Madagascar)</span>

---

### Thesis

**Bloch, Y.** (2026). *A multiscale cellular automata–Markov framework for modelling shifting
cultivation and agroforestry landscapes.* M.Sc. thesis, Department of Life Sciences,
Ben-Gurion University of the Negev. Supervisor: Prof. Shai Pilosof.
<span class="yb-links">[download PDF (8.7 MB)](/research/Bloch_2026_MSc_thesis.pdf) · [code](https://github.com/MadagascarEEID/LUC_Madagascar) · [Zenodo archive](https://doi.org/10.5281/zenodo.21888470)</span>

> Most land-use change models were developed for urban or industrial agricultural landscapes,
> where transitions are broad-scale and long-term. Smallholder shifting cultivation and
> agroforestry operate across multiple spatial and temporal scales, and remain comparatively
> hard to model. I developed a framework that fits landscape-level composition and configuration
> indices — incorporating fractal geometry to capture multiscale structure — rather than relying
> on cell-by-cell spatial agreement. The model was calibrated against observed land-use maps in
> the SAVA region of northeastern Madagascar, then used to project equilibrium landscapes across
> a gradient of agroeconomic scenarios representing increasing reliance on vanilla agroforestry.
> As a proof of concept, the projected landscapes were coupled to a tick population model.

Written up step by step as it was built, including the attempts that did not work — see
[Research](/research/). A retrospective on the three years is in
[Three Years, Six Semesters](/blog/lesson_learn_thesis/).

---

### Software

**LUC_Madagascar** — CA–Markov land-use change model coupled to a stochastic, agent-based tick
population model. Julia; Gillespie simulation, Bayesian optimization (Optuna/TPE), multiscale
lacunarity analysis. Run on Ben-Gurion University's HPC service.
<span class="yb-links">[repository](https://github.com/MadagascarEEID/LUC_Madagascar) · [Zenodo](https://doi.org/10.5281/zenodo.21888470)</span>

**MiRA** — Multilayer Interactive Rendering Application. Browser-based visualization of
multilayer ecological networks, no installation or backend required.
<span class="yb-links">[live application](https://mira.ecomplab.com/) · [preprint](https://arxiv.org/abs/2605.09597)</span>

**Figaro** — built with a team during a lab app-building competition.
<span class="yb-links">[repository](https://github.com/Ecological-Complexity-Lab/figaro-) · [live application](https://ecological-complexity-lab.github.io/figaro-/) · [write-up](/blog/figaro/)</span>

---

### Conference

**Bloch, Y., & Pilosof, S.** (2025). *The Devil Is in the Details: Modeling Small-Scale Land-Use
Change in Madagascar.* Poster.
<span class="yb-links">[extended materials & poster](/research/extended_poster/)</span>

---

### Teaching

Teaching assistant, **Python for Biologists** and **Statistics with Python**, Department of Life
Sciences, Ben-Gurion University (2023–present). Course materials are on the
[teaching](/teaching/) page.
