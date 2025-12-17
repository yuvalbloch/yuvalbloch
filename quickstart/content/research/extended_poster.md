---
title: "The Devil Is in the Details: Modeling Small-Scale Land-Use Change in Madagascar"
date: 2025-12-07
author:
  - Yuval Bloch
  - Shai philosph
contact_email: yuvalblo@postbgu.ac.il
paper_pdf: /reasrch/poster.pdf
omit_header_text: true
enable_toc: true
description: This extended version of the poster I presented in the zoological conference about my research, it includes the poster itself and extensions for each one of them sections
---

## the poster

<iframe src="/reasrch/poster_website_version.pdf" width="100%" height="600px" style="border: none;"></iframe>





## contact info
yuvalblo@postbgu.ac.il




## background and research gap

Land use represents the fundamental interface between humanity and nature. Every human activity, from the urban centers of New York to the remote tribes of the Amazon, involves occupying and altering the environment to meet specific needs. This environment, in turn, critically impacts human well-being: our health, exposure to disease, and vulnerability to natural disasters are intrinsically linked to our surroundings and how we modify them. Land use change is a primary driver of global environmental crises, it the main cause of **85% of endangered species** cases (Hald-Mortensen, 2023), the emergence of **27% of vector-borne zoonotic diseases** (VBZD) (Swei, 2020), it is also the **leading cause of soil loss** (Borrelli, 2017), and accounts for **almost a quarter of greenhouse gases** (Smith, 2014). Predicting how different patterns of land-use change will unfold and affect these processes is crucial for policymakers and stakeholders to develop strategies that minimize adverse impacts on both the environment and human populations.

This human-nature interface is particularly pronounced in smallholder farming systems in tropical, least developed regions, where anthropogenic and natural areas frequently overlap or are mixed in important biodiversity hotspots. However, current research on land-use change prediction prioritizes developed regions characterized by large-scale monocropping. Consequently, the unique land-use patterns of smallholder systems—such as small-scale fragmentation, shifting cultivation, and agroforestry—remain significantly understudied.

  <figure >
    <img src="/reasrch/figure_for_poster/landscape.png" alt="small scale agricultre filed in the study area"        style="max-width: 80%; height: auto; display: block; margin: 0 auto; border-radius: 12px;" >
    <figcaption style="margin-top: 0.5rem; font-size: 0.9rem; color: #555;">
      <strong>Figure 1.</strong> <br> in many least devloped region in the tropics, agricultre and in small, sparse plots, making it challenging to model
    </figcaption>
  </figure>

## Research Objectives

1. **Model future scenarios:** To simulate plausible future land-use change scenarios in the remote SAVA region of Madagascar.
    
2. **Assess disease risk:** To predict the impact of these land-use changes on tick exposure within each scenario, serving as a foundational step in forecasting tick-borne disease dynamics.
## materials and methods 
### study area
The study was conducted in the SAVA region of northeastern Madagascar, specifically in the area surrounding Marojejy National Park. While the SAVA region is the world's primary source of Bourbon vanilla, it remains a remote and economically marginalized area with limited infrastructure. The study focuses on villages bordering the park that are currently in the early stages of market integration.

  <figure >
    <img src="/reasrch/figure_for_poster/study_area.svg" alt="map of the study area"        style="max-width: 80%; height: auto; display: block; margin: 0 auto; border-radius: 12px;" >
    <figcaption style="margin-top: 0.5rem; font-size: 0.9rem; color: #555;">
      <strong>Figure 2.</strong> <br>
    </figcaption>map of the study area
  </figure>

Local agriculture relies on three primary crops: flooded rice, _Tavy_ (shifting cultivation of hill rice), and vanilla agroforestry for commercial sale. _Tavy_ remains the primary driver of deforestation, even within the protected boundaries of Marojejy, due to weak law enforcement. Additionally, the local community cultivates a variety of subsistence crops (Hanke, 2018).

  <figure >
    <img src="/reasrch/figure_for_poster/tavi_cycle.svg" alt="diagram of shifinthig cultivation"        style="max-width: 80%; height: auto; display: block; margin: 0 auto; border-radius: 12px;" >
    <figcaption style="margin-top: 0.5rem; font-size: 0.9rem; color: #555;">
      <strong>Figure 3.</strong> <br>
    </figcaption> Shifting cultivation is a cyclic agriculture practice where forests are burn to fertilize the soil with the ash, which fertilizes the  land alow cultivation crops for short time, but then the land are degraded and the farmer needs to let the forest grow again and then burn it again
  </figure>

The vanilla market acts as the primary driver of market integration in this region. While evidence from similar areas in northeastern Madagascar suggests that cash-crop-based market integration can replace shifting cultivation—potentially reversing the trend from net forest loss to net forest gain—this forest transition has not yet materialized in the SAVA region. 


### modeling future land use change 
We model different levels of transition from shifting cultivation to cash crop agroforestry, under four different assumptions about the agroforestry practice (for simplicity in the poster, I show only scenarios number 2 and 3) 
The scenarios differ in two assumptions: agroforestry degradation and spatial. 

| **Scenario number** | **Vanilla degradation rate** | **Vanilla spatial preference** |
| ------------------- | ---------------------------- | ------------------------------ |
| 1                   | 15 years                     | everywhere                     |
| 2                   | 50 years                     | everywhere                     |
| 3                   | 50 years                     | near village                   |
| 4                   | 200 years                    | near village                   |

### modeling ticks 
We implement the tick model as a four-layer lattice system. The first layer represents land-use types, and the remaining three layers represent tick populations at different life stages (larvae, nymphs, and adults). The model is event-based, with two possible events for each tick:

## result
### land use dissimilarity 
There is no single right way to compare land-use maps, as we must consider two elements: land-use composition and configuration. Moreover, while composition is quite straightforward, as we can use any distance measure, we use the Manhattan distance; configuration is a more complex term, as it behaves differently across scales. We want to account for the level of land-use mixing, so we first calculate the land-use map lacunarity index, which measures the heterogeneity arising from small-scale features (for more information, see https://yuvalbloch.com/research/lacunirty/). If most of the heterogeneity arises at the small scale, it means the land is well mixed and unstructured. By comparing this index across the two scenarios, we can see that at most levels of agroforestry, when vanilla is spread, we obtain much higher index values, indicating greater heterogeneity at the small-scale level. Furthermore, when we compare the heterogeneity index to the dissimilarity in land use composition (both scale from 0 to 1, so we can compare), we see much smaller dissimilarity in the composition, which suggests that the difference in tick exposure drives the configuration rather than the composition. 

### tick exposure
Following the transition from mainly shifting cultivation to mainly cash crops agroforestry, we can see that when the agroforestry plots are spread around, the tick exposure increases until we get to full transition, and then it decreases, but when the agroforestry plots are aggregated near the village, it changes very little acoress partily change and decrese too in full change, this show us that aggregation of the vannila can mitigate the risk during the change, the fact that the diffrent between the secnrio was mainly in configuration and not compostion tell us that it actual realted to the aggreagation of the agroforestry plots


