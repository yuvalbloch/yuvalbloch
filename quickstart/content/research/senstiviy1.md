---
title: "Finding Viable Parameter Spaces with Sensitivity Analysis"
description: "Using machine learning to map the ecological conditions under which tick populations persist or collapse, across a range of ecological and behavioral parameters."
featured_image: "/assets/research/seapration_plane.gif"
tags: [ecological-modeling]
omit_header_text: true
draft: false
date: '2025-06-09T10:00:00+03:00'
---

## Introduction

Ecological models often depend on parameters that are difficult to measure precisely. **Sensitivity analysis** helps us ask: _how much do these uncertainties matter?_ It allows us to explore:

- Which parameters most strongly influence model outcomes
    
- What combinations lead to persistence or extinction
    
- How robust the system is to changes in key assumptions
    

In this project, I go beyond simply measuring sensitivity. I use these tools to **map the boundary between viable and non-viable ecological conditions**—the tipping points where tick populations either collapse or persist. By comparing these boundaries to patterns observed in real-world data, I can ask a deeper question: **which combinations of parameters are not just viable, but actually relevant to the system I'm trying to model?**

---

## Types of Sensitivity Analysis

Throughout this work, I use several types of sensitivity analysis, each suited to a specific goal:

### ❌ Local Sensitivity Analysis  
Changes one parameter at a time.  
**Not used** here—interactions between parameters are too strong for this to be meaningful.

### 🌍 Regional Sensitivity Analysis  
Explores combinations of a few key parameters.  
Used to locate regions where ticks either survive or go extinct under plausible ecological assumptions.

### 🌐 Global Sensitivity Analysis  
Covers the full parameter space.  
Used to identify dominant parameters and how they interact across the entire model.

### 🏞 Structural Sensitivity Analysis  
Varies landscape structure instead of parameters.  
Used to test how spatial patterns (e.g. land use maps) affect tick dynamics.  
_Covered separately due to complexity._

---

## Using SVM to Define the Viable Parameter Space

The first task was to identify which combinations of ecological parameters allow **tick populations to persist**. I focused on three key ones:

- `k`: Carrying capacity  
- `d₀`: Death rate when ticks are rare  
- `d_c`: Death rate at carrying capacity  

I ran many simulations with randomly sampled values for these parameters, labeling the outcomes:

- `0`: Population went extinct  
- `1`: Population persisted  

To organize and generalize these results, I trained a **Support Vector Machine (SVM)**. Rather than just speeding things up, the SVM became central: it **learned the boundary** between survival and extinction and gave me a functional representation of the viable region in parameter space.

---

## Active Learning: Smarter Sampling

To improve the SVM with fewer simulations, I used **active learning**. The model identified parameter sets near the decision boundary—where it was most uncertain—and I focused simulations there.

I tried a few kernel functions and settled on a **polynomial kernel**, which captured the nonlinear shape of the viability boundary best.

---


  <figure style="flex: 1; min-width: 240px; max-width: 400px; text-align: center;">
    <img src="/assets/research/seapration_plane.gif" alt="SVM separation boundary" style="width: 100%; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
    <figcaption style="margin-top: 0.5rem; font-size: 0.9rem; color: #555;">
      <strong>Figure 1.</strong> SVM decision boundary separating viable (persistent) and non-viable (extinct) regions in parameter space.
    </figcaption>
  </figure>


---

## Beyond Viability: Exploring System Behavior

Once I mapped the viability zone, I looked more closely at **how** the model behaves across it. I used three summary statistics:

- **Proportion of occupied cells**  
- **Mean number of ticks per occupied cell**  
- **Overall average tick density**

Many parameter sets produced all-or-nothing results—either nearly all cells were full or nearly all were empty. But real ecosystems aren’t so binary. I was looking for **mixed outcomes**: some patches full, others not. This is what I observed in field data and wanted the model to reflect.

---

<div>
  <figure style="flex: 1; min-width: 240px; max-width: 400px; text-align: center;">
    <img src="/assets/research/1_historgrams.png" alt="Distribution of outcomes" style="width: 100%; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
    <figcaption style="margin-top: 0.5rem; font-size: 0.9rem; color: #555;">
      <strong>Figure 2.</strong> Distribution of simulation outcomes across parameter space. Many combinations lead to near-total persistence or extinction.
    </figcaption>
  </figure>
</div>

---

## Parameter Insights

Looking across the viable space, several patterns became clear:

- **Increasing `d₀`** reduces both:
  - The proportion of occupied cells  
  - The average number of ticks per occupied cell  

- **Increasing `k`** has the opposite effect:
  - It raises both patch occupancy and tick density  

- The **difference between `d₀` and `d_c`** also matters:
  - A larger difference boosts the number of surviving patches  
  - But lowers the average tick count within them—possibly due to early saturation

---

<div>
  <figure style="flex: 1; min-width: 240px; max-width: 400px; text-align: center;">
    <img src="/assets/research/3.input_output_reltionship.png" alt="Input-output relationships" style="width: 100%; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
    <figcaption style="margin-top: 0.5rem; font-size: 0.9rem; color: #555;">
      <strong>Figure 3.</strong> Relationships between model inputs and outputs. Adjusting both $d₀$ and $d_c$ allows control over tick density and landscape heterogeneity.
    </figcaption>
  </figure>
</div>

---

### What I’m Looking For



The real world is not homogeneous. Field data show **variation**—some areas have ticks, others do not—and this pattern holds across different values of _k_. To reflect that, I searched for parameter sets that produced:

- **Heterogeneous landscapes** with partial tick occupancy
    
- **Moderate tick densities** that avoid unrealistic overpopulation
    

After testing many combinations, I identified one that struck a good balance. Tick populations persisted **in some** areas while remaining ecologically realistic, closely aligning with observed dynamics.

---

<div>
  <figure style="flex: 1; min-width: 240px; max-width: 400px; text-align: center;">
    <img src="/assets/research/2_ocupied_cell_proprtion_group.png" alt="Occupied cell proportion" style="width: 100%; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);">
    <figcaption style="margin-top: 0.5rem; font-size: 0.9rem; color: #555;">
      <strong>Figure 4.</strong> Occupied cell proportions grouped by $k$ and a linear combination of $d₀$ and $d_c$. This tuning expands the range of $k$ values with realistic spatial heterogeneity.
    </figcaption>
  </figure>
</div>




The final question I need to answer before applying this model to real land use scenarios is whether it responds only to **average carrying capacity**—or if it's also sensitive to the **structure of the landscape** itself. This matters because research shows that spatial structure can strongly influence tick populations, yet it’s much harder to capture in models.

In my [next post](https://yuvalbloch.com/research/sensitivity-to-land-configuration/), I’ll explore this by using a beautiful mathematical concept: **fractal dimensionality**. I’ll show how it reveals that the model isn’t just reacting to average conditions—it’s truly sensitive to the **spatial complexity** of the land.

📢 **Stay tuned**—it gets surprisingly elegant.


{{< repo >}}
