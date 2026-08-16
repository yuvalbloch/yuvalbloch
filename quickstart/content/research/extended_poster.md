---
title: "The Devil Is in the Details: Modeling Small-Scale Land-Use Change in Madagascar"
date: 2025-12-07
tags: [ecological-modeling, academic-life]
author:
  - "Yuval Bloch"
  - "Shai Pilosof"
contact_email: "yuvalblo@postbgu.ac.il"
paper_pdf: "/research/poster.pdf"
omit_header_text: true
enable_toc: true
description: "Extended research materials for the zoological conference poster: Modeling smallholder land-use patterns and tick-borne disease risks in Madagascar."
---

## 🖼️ The Poster
If you are viewing this on a mobile device, you can view the full PDF below or [**Download the PDF here**](/research/poster_website_version.pdf).

<iframe src="/research/poster_website_version.pdf" width="100%" height="600px" style="border: 2px solid #eee; border-radius: 8px;"></iframe>

---

## 📌 Introduction & Research Gap

Land use represents the fundamental interface between humanity and nature. From urban centers to remote tropical regions, environmental modification critically affects human health, disease exposure, and vulnerability to natural disasters. 

**Land-use change is a primary driver of global crises:**
* **85%** of endangered species cases (Hald-Mortensen, 2023).
* **27%** of emerging vector-borne zoonotic diseases (VBZD) (Swei, 2020).
* **Leading cause** of global soil loss (Borrelli, 2017).
* **~25%** of global greenhouse gas emissions (Smith, 2014).

### The "Small-Scale" Challenge
Most land-use prediction models focus on large-scale monocropping in developed regions. However, in tropical biodiversity hotspots like Madagascar, land use is dominated by **smallholder farming systems**. These systems involve complex patterns—fragmentation, shifting cultivation, and agroforestry—that remain significantly understudied. Furthermore, in those areas, anthropogenic and natural land uses overlap extensively, underscoring the need to model them.

<figure>
  <img src="/research/figure_for_poster/landscape.png" alt="Small-scale agriculture field in Madagascar" style="max-width: 90%; height: auto; display: block; margin: 0 auto; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <figcaption style="text-align: center; margin-top: 0.8rem; font-size: 0.9rem; color: #555;">
    <strong>Figure 1.</strong> In many tropical regions, agriculture exists in small, sparse plots, making them difficult to model with standard tools.
  </figcaption>
</figure>

---

## 🎯 Research Objectives

1.  **Model Future Scenarios:** Simulate plausible land-use changes in the remote SAVA region of Madagascar.
2.  **Assess Disease Risk:** Predict how these changes impact **tick exposure**, providing a foundation for forecasting tick-borne disease dynamics.

---

## 🛠️ Materials and Methods

### Study Area: The SAVA Region
The study focuses on villages bordering **Marojejy National Park**. While the SAVA region is the global hub for Bourbon vanilla, it remains economically marginalized with limited infrastructure.

<figure>
  <img src="/research/figure_for_poster/study_area.svg" alt="Map of the study area" style="max-width: 90%; height: auto; display: block; margin: 0 auto; border-radius: 12px;">
  <figcaption style="text-align: center; margin-top: 0.8rem; font-size: 0.9rem; color: #555;">
    <strong>Figure 2.</strong> Map of the study area surrounding Marojejy National Park.
  </figcaption>
</figure>

**Agricultural Practices:**
* **Flooded Rice:** Staple subsistence.
* **Tavy:** Shifting cultivation (slash-and-burn), the primary driver of deforestation.
* **Vanilla Agroforestry:** The main cash crop and driver of market integration.

<figure>
  <img src="/research/figure_for_poster/tavi_cycle.svg" alt="Diagram of shifting cultivation cycle" style="max-width: 80%; height: auto; display: block; margin: 0 auto;">
  <figcaption style="text-align: center; margin-top: 0.8rem; font-size: 0.9rem; color: #555;">
    <strong>Figure 3. The Tavy Cycle.</strong> A cyclic practice where forest is burned to fertilize soil. After short-term cultivation, the land degrades, requiring a fallow period for forest regrowth before the cycle repeats.
  </figcaption>
</figure>

### Modeling Future Scenarios
We modeled the transition from shifting cultivation to vanilla agroforestry using four scenarios based on **degradation rates** and **spatial preference**.

| Scenario | Vanilla Degradation Rate | Spatial Preference |
| :--- | :--- | :--- |
| **1** | 15 years | Everywhere |
| **2 (Selected)** | 50 years | Everywhere |
| **3 (Selected)** | 50 years | Near Villages |
| **4** | 200 years | Near Villages |

> **Note:** This presentation focuses on **Scenarios 2 and 3** to highlight how spatial configuration (where crops are planted) affects risk.

<figure> <img src="/research/figure_for_poster/secnrios.svg" alt="Comparison of scenario assumptions for agroforestry spatial preference" style="max-width: 80%; height: auto; display: block; margin: 0 auto; border-radius: 12px;"> <figcaption style="margin-top: 0.5rem; font-size: 0.9rem; color: #555;"> <strong>Figure 4.</strong> Poster focus: Scenarios 2 and 3 differ in agroforestry spatial preference (spread vs. clustered near villages). We evaluate multiple transition levels within each scenario. </figcaption> </figure>



### The Tick Population Model
We implemented a four-layer lattice system to simulate tick dynamics:
1.  **Layer 1:** Land-use types.
2.  **Layers 2-4:** Tick life stages (larvae, nymphs, and adults).

Ticks move between life stages and across the landscape by interacting with hosts. [Read more about the model technicalities here](https://yuvalbloch.com/research/tick-population-model/).


<figure> <img src="/research/figure_for_poster/tick_model.svg" alt="Diagram of the tick lattice model with life stages" style="max-width: 80%; height: auto; display: block; margin: 0 auto; border-radius: 12px;"> <figcaption style="margin-top: 0.5rem; font-size: 0.9rem; color: #555;"> <strong>Figure 5.</strong> Tick model: three population layers (larvae, nymphs, adults) interacting across space and transitioning between life stages via host interactions. </figcaption> </figure>

---

## Results

### Land-use dissimilarity: composition vs. configuration

There is no single “best” way to compare land-use maps. We separate differences into:

- **Composition:** how much of each land-use type exists (measured with **Manhattan distance**, scaled 0–1)
    
- **Configuration:** how those land uses are arranged across space (captured with a **lacunarity-based heterogeneity index**)
    

We use lacunarity because we specifically want to detect heterogeneity arising from **small-scale mixing**. Across transition levels, the “spread” vanilla scenario shows higher small-scale heterogeneity—indicating more mixing and less spatial structure.

Comparing the two indices (both scaled 0–1), we find that composition differences are smaller than configuration differences, suggesting that, in this case, changes in results driven by tick exposure are more attributable to how land uses are arranged than to the overall proportions.

More on lacunarity here:  
[Lacunarity](https://yuvalbloch.com/research/lacunirty/)

<figure>
  <img src="/research/figure_for_poster/land_result.svg" alt="Land use results graph" style="max-width: 90%; height: auto; display: block; margin: 0 auto;">
  <figcaption style="text-align: center; margin-top: 0.8rem; font-size: 0.9rem; color: #555;">
    <strong>Figure 6.</strong> Differences in tick exposure are driven by land configuration (mixing) rather than simple changes in land proportions.
  </figcaption>
</figure>

### 2. Tick Exposure Risk
Our model shows that the **spatial aggregation** of vanilla agroforestry is a critical lever for public health:
* **Spread-out Vanilla:** Tick exposure increases significantly during the transition to agroforestry.
* **Aggregated Vanilla (Near Villages):** Risk is mitigated throughout the transition.

**Conclusion:** Concentrating agroforestry plots near existing settlements can reduce human-tick contact rates during economic transitions.

<figure>
  <img src="/research/figure_for_poster/ticks_result.svg" alt="Tick exposure results graph" style="max-width: 90%; height: auto; display: block; margin: 0 auto;">
  <figcaption style="text-align: center; margin-top: 0.8rem; font-size: 0.9rem; color: #555;">
    <strong>Figure 7.</strong> Aggregating vanilla plots near villages mitigates tick exposure risk during the transition from shifting cultivation.
  </figcaption>
</figure>

---

## 📧 Contact Information
**Yuval Bloch** Ben-Gurion University of the Negev  
Email: [yuvalblo@postbgu.ac.il](mailto:yuvalblo@postbgu.ac.il)

---

## 📚 References
* **Borrelli, P., et al. (2017).** An assessment of the global impact of 21st-century land use change on soil erosion. *Nature Communications*, 8(1), 2013.
* **Hald-Mortensen, C. (2023).** The main drivers of biodiversity loss: A brief overview. *Journal of Ecology & Natural Resources*.
* **Hänke, H., et al. (2018).** *Socio-economic, land use and value chain perspectives on vanilla farming in the SAVA Region*. Diskussionsbeitrag No. 1806.
* **Mariel, J. et al. (2023).** From shifting rice cultivation (Tavy) to agroforestry systems. *Agroforestry Systems*, 97(3), 415–431.
* **Smith, P., et al. (2014).** Agriculture, Forestry and Other Land Use (AFOLU). *IPCC AR5*.
* **Swei, A., et al. (2020).** Patterns, drivers, and challenges of vector-borne disease emergence. *Vector-Borne and Zoonotic Diseases*, 20(3), 159–170.