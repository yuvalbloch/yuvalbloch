---
title: "End of Greatness: Lacunarity and the Index of Transitional Homogeneity"
description: The scientific journey is built on trial and error. After finding that a standard land-use index wasn't sufficient, I discovered the Index of Transitional Homogeneity (ITH)—and learned a lesson in the beauty of multidisciplinary science.
featured_image: /research/night_sky.jpeg
date: 2026-02-20
tags: [ecological-modeling]
omit_header_text: true
---

One of the best things about being an ecologist in this era is the constant opportunity to bridge different disciplines. Recently, my research led me to use a measure called **transitional homogeneity**—a concept originally developed in cosmology to estimate how matter is spread throughout the universe. My journey to this point was a classic scientific process of trial and error.

### The Quest for a Multi-Scale Metric

After building a cellular automata model to generate future land-use maps, I needed a way to quantify the structural differences between various scenarios. Traditional indices, such as **edge density** (the total length of edges between different land uses), only provide a small part of the picture. They focus on local interactions—representing the contact between two land-use types—without considering the broader landscape context 

Fractal theory provided a potential solution. Tropical deforestation and landscape patterns often behave like fractals over certain scales (Taubert et al., 2018). This means we can quantify their complexity using a measure called **lacunarity**. I initially attempted to use a lacunarity-based heterogeneity index developed by Scott et al. (2022). I recommend reading my [previous post on lacunarity basics](https://yuvalbloch.com/research/lacunirty/) first for a deeper explanation of the concept.

### Problems with the First Attempt: The Correlation Trap

In my first attempt, I converted my land-use maps into edge maps and followed the methodology of Scott et al. to calculate a heterogeneity index. However, when I tested those results against the maps I had created for the sensitivity analysis of my [tick model](https://yuvalbloch.com/research/sensitivity-to-land-configuration/), I discovered that the measurement was highly correlated with simple edge density. 

While the authors of the original paper suspected this correlation might be system-specific, a closer look at the mathematics suggested a more fundamental issue with the normalization.

#### The Math of Lacunarity

Let $X_r$ be a vector containing the sum of data points within every possible sliding window of size $r$ that fits within a map. The lacunarity at scale $r$, $\Lambda(r)$, is defined as:

$$\Lambda(r) = \frac{\text{Var}(X_r)}{\mu(X_r)^2} + 1$$

For binary data (like an edge map), at the smallest scale ($r=1$), the lacunarity $\Lambda(1)$ is essentially determined by the density of the points ($\lambda$). Specifically, $\Lambda(1) = 1/\lambda + 1$. As the window size $r$ increases and approaches the size of the map, the variance drops toward zero and the lacunarity approaches 1.

Scott et al. attempted to normalize this by dividing the values by $\Lambda(1)$. However, because the weighted average they used to create a single index gives significant weight to higher scales—which are themselves constrained by the starting density—the resulting index remains strongly correlated with the simple density of the map.

### A Second Attempt: The Index of Transitional Homogeneity (ITH)

Identifying the normalization problem led me to the work of **Malhi & Román-Cuesta (2008)**. They proposed a different normalization method using logarithms:

$$\hat{\Lambda}(i) = \frac{\ln(\Lambda(i))}{\ln(\Lambda(1))}$$

This approach ensures $\hat{\Lambda}(i)$ ranges between 1 and 0 and is significantly less correlated with density. More importantly, they introduced a different metric: the **Index of Transitional Homogeneity (ITH)**.

#### From Galaxies to Trees: The "End of Greatness"

The logic behind ITH is fascinatingly interdisciplinary. In cosmology, scientists ask how matter is distributed in the universe. At the scale of solar systems or galaxies, matter is highly concentrated (clumped). However, at a large enough scale—known as the scale of **transitional homogeneity** (sometimes called the "End of Greatness")—the distribution of matter becomes essentially random and uniform.

Malhi & Román-Cuesta applied this to forest canopies, asking at what scale the spread of an ecological property (like tree crowns or photosynthesis) becomes homogeneous. 

<figure>
  <img src="/research/night_sky.jpeg" alt="night sky" style="max-width: 60%; height: auto; display: block; margin: 0 auto; border-radius: 12px;">
  <figcaption style="font-size: 0.9em; font-style: italic; color: #555; margin-top: 1.5rem; margin-bottom: 1.5rem; line-height: 1.4; text-align: center; border-top: 1px solid #ccc; padding-top: 1rem;">
    A simple look at the night sky reveals that stars are not distributed homogeneously; they are clustered into the disk of the Milky Way. ITH helps us find the scale where such clustering gives way to uniformity.
  </figcaption>
</figure>

### How ITH Works

To calculate ITH, we plot the normalized lacunarity curve on a logarithmic scale. In most landscapes, a linear section of the curve represents "fractal" behavior. By extrapolating this line to the axis where normalized lacunarity reaches zero (homogeneity), we identify the physical scale at which the fractal structure ends. 

Unlike abstract indices, ITH has a clear physical meaning and unit: it represents the **characteristic size of the geometric objects** (or clumps) in the landscape.



<figure>
  <img src="/research/methods_land_use_analsys.svg" alt="examples of ITH calculation" style="max-width: 60%; height: auto; display: block; margin: 0 auto; border-radius: 12px;">
  <figcaption style="font-size: 0.9em; font-style: italic; color: #555; margin-top: 1.5rem; margin-bottom: 1.5rem; line-height: 1.4; text-align: center; border-top: 1px solid #ccc; padding-top: 1rem;">
    <strong>Land-use configuration analysis:</strong> (a) Comparison of two maps with identical compositions but different arrangements. (b) Edge maps showing differences in edge density. (c) Variance in density decreases as window size $r$ increases. (d) Normalized lacunarity shows Map 1 loses variance faster due to its single characteristic scale. (e) Extrapolating the fractal region of a real land-use map yields the ITH scale.
  </figcaption>
</figure>

### Using ITH in My Research

In my thesis, I compared different scenarios for the transition from shifting cultivation (*tavy*) to agroforestry in the SAVA region of northeastern Madagascar. While land composition and edge density were primarily sensitive to the simple balance of crops, ITH provided a much richer picture. 

I found that ITH was sensitive to all key parameters: the amount of agroforestry, its stability over time, and the spatial preference for clustering near villages. More stable and clustered agricultural patterns led to higher ITH values, as they allowed for the development of more significant, multi-scale landscape structures.

This evolution—moving from simple interaction indices to complex, multidisciplinary structures—is a trend we see across all of modern ecology. Whether it is using **network theory** (inspired by the architecture of the internet) to understand species interactions, or applying **physics-driven models** of regime shifts to predict ecosystem stability, these borrowed tools allow us to see further than ever before. By looking at the landscape through the lens of other disciplines, we don't just see pixels or edges; we see the underlying logic of the systems we study.

---

## Resources

* **Scott, R., et al. (2022).** [A Lacunarity-based Index for Spatial Heterogeneity.](https://doi.org/10.1029/2021ea002180) *Earth and Space Science*.
* **Taubert, F., et al. (2018).** Global patterns of tropical forest fragmentation. *Nature*, 554(7693), 519–522.
* **Malhi, Y. & Román-Cuesta, R. M. (2008).** [Analysis of lacunarity and scales of spatial homogeneity in IKONOS images of Amazonian tropical forest canopies.](https://doi.org/10.1016/j.rse.2008.01.001) *Remote Sensing of Environment*.