---
lang: "en"
title: "Sensitivity to Land Configuration"
description: "To ensure that my model accurately captures the impact of land configuration, I incorporate the diamond-square algorithm and the concept of fractal dimensionality. While these tools are unconventional for this purpose, they provide a robust and meaningful way to model spatial complexity and the effects of landscape structure."
featured_image: "/assets/research/fractal_landscape.jpeg"
tags: [ecological-modeling]
omit_header_text: true
draft: false
date: '2025-07-07T10:00:00+03:00'
---

## Introduction

Natural populations are influenced not only by the **amount** of available habitat but also by its **spatial configuration**. Factors such as **edge effects**, **habitat fragmentation**, and **patch isolation** are critical in shaping population dynamics. These spatial processes are fundamental in ecology, and it's essential that my model captures them accurately.

While the total amount of habitat is relatively easy to quantify, capturing spatial configuration is far more complex. Traditional models often rely on a **binary landscape**, classifying areas as either suitable or unsuitable for the organism. Metrics like **edge length**, **connectivity**, and **mean patch size** are often used in these models. However, in my system, the landscape consists of multiple land cover types, each offering varying degrees of suitability for ticks. This complexity demands a more nuanced and flexible approach.

The framework provided by **Tracey, Bevins, VandeWoude, and Crooks (2014)** is particularly useful. Although their model uses binary land classification, they introduce the concept of **fractal dimensionality**, which can be adapted to multi-type habitat systems.

---

## Fractal Dimensionality

In _On Exactitude in Science_, Jorge Luis Borges imagines an empire where the map created by cartographers is as vast as the empire itself. This allegory highlights a crucial point in spatial modeling: the more we examine a landscape, the more complex it becomes, making it harder to measure and represent.

A real-world example of this is **Benoît Mandelbrot’s** question: _“How long is the coast of Britain?”_ At low resolution, the coastline appears smooth. However, as resolution increases, more features, such as inlets and jagged rocks, emerge, causing the measured length to increase. This illustrates that some natural features defy classical Euclidean geometry and are better modeled using **fractal geometry**.

To quantify this complexity, we use the **Hurst exponent (H)** or the **fractal dimension (Hausdorff dimension) (D)**. These parameters describe how spatial roughness increases with resolution. Importantly, the **H** value also captures the degree of **mixing** between spatial domains.

For example, when land and sea are clearly separated, the boundary is simple and H is low. As the boundary becomes more complex, with features like bays and estuaries, H increases. Hence, **H** serves as a proxy for **spatial mixing or interlacing**.

This concept extends beyond coastlines to **topographic variation** (e.g., mountains vs. flatlands) and anthropogenic gradients (e.g., from natural forest to urbanized land). High H values reflect greater spatial complexity and aggregation, while low H values indicate fragmented or randomized patterns.

  <figure >
    <img src="/assets/research/coast_line.png" alt="Coastline"        style="max-width: 80%; height: auto; display: block; margin: 0 auto; border-radius: 12px;" >
    <figcaption style="margin-top: 0.5rem; font-size: 0.9rem; color: #555;">
      <strong>Figure 1.</strong> <br> A coastline viewed from above. As the resolution increases, more intricate bays and inlets become visible.
    </figcaption>
  </figure>


---

## Generating Fractal Landscapes

To produce landscapes with varying levels of spatial complexity, I use the **diamond-square algorithm**, a two-dimensional extension of the **midpoint displacement algorithm**. These methods generate fractal surfaces that mimic the irregularity and patchiness found in real-world habitats.

### Midpoint Displacement Algorithm

### Midpoint Displacement Algorithm

The **Midpoint Displacement Algorithm** is a simple yet powerful method for generating fractal-like patterns. It starts with a straight line or a grid and recursively introduces randomness to create jagged, irregular structures. Here’s how it works:

1. **Initial Setup**: Start with two points (for 1D) or four corner points (for 2D).
    
2. **First Midpoint**: Calculate the midpoint between two points, adding a random displacement. This creates an irregularity in the line or surface.
    
3. **Recursive Process**: The line or grid is recursively divided into smaller segments, and each midpoint is displaced by a random value.
    
4. **Decreasing Displacement**: As the algorithm proceeds, the magnitude of the random displacement decreases, usually scaled by 2−H2^{-H}2−H, where **H** is the **Hurst exponent**, controlling roughness.
    

Over several iterations, the line or surface becomes jagged and self-similar, mimicking natural irregular features like coastlines or mountain ridges.

For more information, you can check out the detailed explanation on [Landscape Generation Using Midpoint Displacement](https://bitesofcode.wordpress.com/2016/12/23/landscape-generation-using-midpoint-displacement/).

#### Applications:

- **Terrain Generation**: Often used in computer graphics and video games to create natural-looking landscapes.
    
- **Fractal Patterns**: Ideal for modeling fractal curves, such as coastlines, rivers, and ridgelines.

### Diamond-Square Algorithm

To extend the midpoint displacement algorithm to two dimensions, we use the **diamond-square algorithm**, which applies recursive steps to refine a square grid, generating a fractal surface. Let’s consider a simple 3×3 grid (a portion of a larger grid) where the numbers represent the values at each position:

```

1 ? 2  
? x ?  
3 ? 4

```

Here, the `x` represents the center of the square, which we calculate using the **diamond step**. The grid is recursively refined, adding more detail and introducing **random offsets** to generate the fractal structure. This process consists of two primary steps: the **diamond step** and the **square step**.

#### Step 1: Diamond Step

In the **diamond step**, we calculate the value at the center of each square formed by four adjacent grid points. For example, to calculate the value at the center (position `x`), we average the four corner values of the square (positions 1, 2, 3, and 4) and add a random offset:

```

x = (1 + 2 + 3 + 4) / 4 + random offset = 3 + random offset

```

The random offset introduces variability, and as the algorithm progresses, its magnitude decreases, typically scaled by \(2^{-H}\), where **H** is the **Hurst exponent** that controls the roughness of the landscape.

#### Step 2: Square Step

```

1  ?  2  
? 3.5 y  
3  ?  4

```

After the diamond step, we move on to the **square step**, where we calculate the midpoints of the edges of the squares formed. For example, to calculate the midpoint at position `y` we average the values of the surrounding points and add another random displacement:

```

y = (2 + 3.5 + 4 ) / 3 + random offset

```

The square step is applied to all edge midpoints in the grid. At each step, a random offset is added, and its magnitude decreases with each iteration, according to \(2^{-H}\). The value of **H** influences the surface roughness:

- **Low H values** produce jagged, fragmented patterns (more irregular).
- **High H values** create smoother, more aggregated surfaces.

This iterative process continues, refining the grid until the desired level of complexity is reached.

---

## Discretizing the Gradient

Once the fractal landscape is generated, I convert the continuous values into a **discrete land-use map**. For example, in the last line of the figure land-use types are assigned as follows:

- The top 10% of values become **villages**,
- The next 30% become **agriculture**,
- The next 30% is **secondary forest**,
- The lowest 30% is **semi-intact forest**.

In the generated maps, **high H values** lead to **spatially clustered patches** of the same land-use type, while **low H values** result in more scattered and mixed distributions.


  <figure >
    <img src="/assets/research/land_use_configuration.svg" alt="Land Use Configuration"        style="max-width: 80%; height: auto; display: block; margin: 0 auto; border-radius: 12px;">>
    <figcaption style="margin-top: 0.5rem; font-size: 0.9rem; color: #555;">
      <strong>Figure 2.</strong> <br> Different land-use configurations based on H values and land-use proportions.
    </figcaption>
  </figure>


---

## Simulation Results

Below is a plot of the **average tick abundance** in each land-use type as a function of the **H value** used to generate the map. As expected, the **total tick population increases with H**, likely due to reduced fragmentation and better connectivity of suitable habitat.

Interestingly, the **average number of ticks in villages** decreases as H increases. This result aligns with the **edge effect hypothesis**: in fragmented landscapes (low H), ticks spill over into marginal patches, while in aggregated landscapes (high H), the boundaries between suitable and unsuitable land-use types are reduced, leading to lower tick numbers in marginal areas.


  <figure>
    <img src="/assets/research/ticks_in_land_use.svg" alt="Tick Population in Land Use"        style="max-width: 80%; height: auto; display: block; margin: 0 auto; border-radius: 12px;">>
    <figcaption style="margin-top: 0.5rem; font-size: 0.9rem; color: #555;">
      <strong>Figure 3.</strong> <br> Tick abundance as a function of H, both in average and in each land-use type.
    </figcaption>
  </figure>


---

### Summary

These results confirm that the model is **sensitive to spatial configuration** and behaves in ways consistent with ecological theory. By using fractal geometry and varying H values, I can simulate more realistic landscape structures and test how fragmentation and habitat mixing impact tick populations.

In the next post, I will explore how spatial complexity further influences model behavior and provide additional insights into the ecological processes shaping these patterns.



{{< repo >}}
