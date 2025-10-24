---
title: Explaining the Lacunarity-Based Index for Spatial Heterogeneity
featured_image: /images/fractal.jpg
date: 2025-10-22
description: This technical post provides a comprehensive explanation of the Lacunarity-Based Index for Spatial Heterogeneity from Scott, R., et al. (2022). It covers the core concept of $\Lambda(r)$ (lacunarity at scale $r$), details the derivation of the standardized single index ($h$), presents a clear step-by-step toy example on binary maps, and provides a simple, functional Julia implementation for calculating the index across scales.
draft: false
omit_header_text: true
---


In my research, I employ the measurement of **lacunarity** based on the methodology described in Scott, R., et al. **"A Lacunarity-based Index for Spatial Heterogeneity."** _Earth and Space Science (Hoboken, N.J.)_, vol. 9, no. 8, American Geophysical Union (AGU), Aug. 2022, [https://doi.org/10.1029/2021ea002180](https://doi.org/10.1029/2021ea002180).

Here, I will provide a less formal description of the mathematics behind this method and its implementation in **Julia**.

---

## 1. What is Lacunarity ($\Lambda(r)$)?

**Lacunarity** is a measure of the **heterogeneity** (gaps and clustering) of a spatial pattern across different scales. It quantifies how much the distribution of features differs from a homogeneous, uniform distribution.

The lacunarity at a specific scale $r$ (the box size) is calculated using the statistics of the sliding-window sums.

Let $X_r$ be the vector containing the **sum** of data points within every possible sliding window of size $r$ that fits within the map. The formula for lacunarity at scale $r$, $\Lambda(r)$, is defined as:

$$\Lambda(r) = \frac{\text{Var}(X_r)}{\mu(X_r)^2} + 1$$

In this formula, $\mu(X_r)$ is the mean of the window sums, and $\text{Var}(X_r)$ is the variance of the window sums.

### Toy Example

Consider two $3 \times 3$ binary maps, where the numbers represent the presence (1) or absence (0) of a feature:

<figure>
    <table>
        <thead>
            <tr>
                <th style="text-align: center;">Structured Map   |   </th>
                <th style="text-align: center;">Homogeneous Map</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td style="text-align: center;"><code>0 0 0</code></td>
                <td style="text-align: center;"><code>0 1 0</code></td>
            </tr>
            <tr>
                <td style="text-align: center;"><code>0 1 1</code></td>
                <td style="text-align: center;"><code>1 0 1</code></td>
            </tr>
            <tr>
                <td style="text-align: center;"><code>0 1 1</code></td>
                <td style="text-align: center;"><code>0 1 0</code></td>
            </tr>
        </tbody>
    </table>

</figure>


**Case 1: Box Size** $r = 1$

Each box includes only one data point. For both maps, we have nine values: five $0$'s and four $1$'s.

- Mean $\mu(X_1) = 4/9 \approx 0.444$
    
- Variance $\text{Var}(X_1) = \mu(X_1^2) - \mu(X_1)^2 = 4/9 - (4/9)^2 \approx 0.2469$
    
- Lacunarity $\Lambda(1) = \frac{0.2469}{0.444^2} + 1 \approx 2.250$
    

Since the distribution of values is identical (four 1s, five 0s), $\Lambda(1)$ is the same for both maps.

**Case 2: Box Size** $r = 2$

We now slide a $2 \times 2$ window across the $3 \times 3$ map, resulting in four possible window sums ($X_2$).



<figure>
    <table>
        <thead>
            <tr>
                <th style="text-align: center;">Structured Map   |   </th>
                <th style="text-align: center;">Homogeneous Map</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td style="text-align: center;"><code>1 2</code></td>
                <td style="text-align: center;"><code>2 2</code></td>
            </tr>
            <tr>
                <td style="text-align: center;"><code>2 4</code></td>
                <td style="text-align: center;"><code>2 2</code></td>
            </tr>
        </tbody>
    </table>

</figure>

**Structured Map Analysis:**

- $X_2 = [1, 2, 2, 4]$
    
- Mean $\mu(X_2) = (1+2+2+4) / 4 = 9/4 = 2.25$
    
- $\text{Var}(X_2) = \frac{(1^2+2^2+2^2+4^2)}{4} - (2.25)^2 = 6.25 - 5.0625 = 1.1875$
    
- $\Lambda(2) = \frac{1.1875}{2.25^2} + 1 \approx 1.234$
    

**Homogeneous Map Analysis:**

- $X_2 = [2, 2, 2, 2]$
    
- Mean $\mu(X_2) = 2$
    
- $\text{Var}(X_2) = 0$
    
- $\Lambda(2) = \frac{0}{2^2} + 1 = 1.000$
    

The results clearly show that at scale $r=2$, the **Structured Map** remains heterogeneous ($\Lambda(2) > 1$), while the **Homogeneous Map** is perfectly uniform ($\Lambda(2) = 1$).

### General Behavior

At $r = 1$, lacunarity reflects only the local variation in pixel values, and is **indifferent to spatial structure**.

As $r$ increases, $\Lambda(r)$ generally decreases. However, in **structured maps**, this decrease is slower because patterns persist across scales. When $\Lambda(r)=1$, it means the map appears homogeneous at that scale. If $\Lambda(r)$ doesn't reach 1 before the sliding window size approaches the map size, it suggests the map is not large enough to fully capture the spatial configuration.

---

## 2. Deriving the Single Heterogeneity Index ($h$)

Lacunarity provides a **curve** showing heterogeneity across scales (a log-log plot of $\Lambda(r)$ vs. $r$). To easily compare multiple maps, this curve must be condensed into a single, standardizable index $h$.

The calculation involves three steps:

### A. Calculating the Scale-Integrated Measure ($R$)

This step integrates the lacunarity curve over a chosen range of box sizes (from $r=1$ up to $N$) while giving more weight to larger scales.

$$R = \frac{1}{N} \cdot \sum_{r=1}^{N} r \cdot \frac{\Lambda(r)}{\Lambda(1)}$$

1. **Normalization (**$\frac{\Lambda(r)}{\Lambda(1)}$**):** Dividing by $\Lambda(1)$ standardizes the values, removing the bias related to the overall frequency of the features.
    
2. **Weighting (**$r$**):** Multiplying by $r$ gives **higher weight to larger box sizes**. This ensures that larger spatial structures have a greater impact on the final index.
    
3. **Averaging (**$\frac{1}{N}$**):** Dividing by $N$ (the number of scales tested) provides an average integrated measure.
    

### B. Standardization

To allow for meaningful comparison between maps of different sizes or scale ranges, $R$ must be standardized by the maximum possible value it could achieve ($R_{\text{max}}$). This maximum is theoretically achieved in a perfectly **homogeneous system** where $\Lambda(r)=1$ for all $r$.

The sum of $r$ from $1$ to $N$ is the arithmetic series $\sum r = \frac{N(N+1)}{2}$.

$$R_{\text{max}} = \frac{1}{N} \cdot \sum_{r=1}^{N} r \cdot \frac{1}{1} = \frac{1}{N} \cdot \frac{N(N+1)}{2} = \frac{N+1}{2}$$

### C. Calculating the Final Index ($h$)

The standardized measure $\frac{R}{R_{\text{max}}}$ peaks at 1 for a perfectly homogeneous map. The Scott et al. (2022) paper aims for a **heterogeneity** index, so they invert the result:

$$h = 1 - \frac{R}{R_{\text{max}}} = 1 - \frac{2 \cdot R}{N+1}$$

- **Interpretation of** $h$**:**
    
    - $h=0$: Perfectly **homogeneous** system (minimal heterogeneity).
        
    - $h$ near 1: Highly **heterogeneous** or chaotic system (maximal heterogeneity).
        
    - Intermediate $h$: A structured system.
        

In fractal landscapes, $h$ increases with fractal complexity. In midpoint displacement models, a **lower** $h$ suggests smoother, less mixed surfaces (higher Hurst parameters).

---

## Application in My Work

I will use this index $h$ to connect the **structure sensitivity analyses** to the base and future scenarios in my work. The base scenarios have already been fitted using boundary lacunarity. By measuring the $h$ index in the structure sensitivity analysis and the future maps, I can establish a clear framework.

This will allow me to create a clear framework where the variance in predicted tick populations can be separated into components:

1. **Explained by land distribution** (e.g., overall land composition).
    
2. **Explained by land use lacunarity** (the $h$ index, reflecting spatial configuration).
    
3. **Unexplained** (residual variance).
    

---

## Implementation in Julia

To calculate lacunarity, we first need to find the sum of the values in sliding windows of size $r$.



``` julia
function box_sum(B_map, r)

    nrows, ncols = size(B_map)

    # The result map has dimensions (Map_Rows - r + 1) x (Map_Cols - r + 1)
    sum_box = zeros(Int, nrows - r + 1, ncols - r + 1)

    @inbounds for i in 1:(nrows-r+1)

        for j in 1:(ncols-r+1)

            # Sum the values in the current sliding window
            sum_box[i, j] = sum(B_map[i:(i+r-1), j:(j+r-1)])

        end

    end

    return sum_box

end
```

Then, we can use the window sums to calculate the lacunarity at that specific scale:



``` julia
function calcualte_lacunrity(B_map, r)

    sum_box = box_sum(B_map, r)

    # We need the mean and the *uncorrected* variance (population variance)
    mean_val = mean(sum_box)

    # The 'corrected=false' argument calculates the population variance
    variance_val = var(sum_box; corrected=false)

    # Lacunarity formula: 1 + Var(Xr) / Mu(Xr)^2
    lacunarity = 1 + variance_val / (mean_val^2)

    return lacunarity

end
```

Next, we calculate the lacunarity across a range of box sizes. Note that while the paper uses every possible value of $r$, I sample scales only at powers of two, as I frequently work with large maps. This impacts the subsequent calculation of $R_{\text{max}}$.



``` julia
function lacunrity_across_r(B_map, max_r=-1)

    if max_r == -1

        max_r = min(size(B_map)...)

    end

    lacunarity_values = DataFrames.DataFrame(r=Int[], lacunarity=Float64[])

    r = 1

    while r < max_r

        lacunarity = calcualte_lacunrity(B_map, r)

        push!(lacunarity_values, (r=r, lacunarity=lacunarity))

        r *= 2 # Increment r by powers of two

    end

    return lacunarity_values

end
```

Finally, we calculate the single heterogeneity index $h$:



``` julia
function calcualte_index(B_map)

    lacunarity_values = lacunrity_across_r(B_map)

    lac_1 = lacunarity_values[1, :lacunarity]

    N = nrow(lacunarity_values)

    R = 0 # Scale-Integrated Measure

    R_max = 0 # Maximum possible R based on sampled r values

    for row in 1:N

        current_r = lacunarity_values[row, :r]

        current_lac = lacunarity_values[row, :lacunarity]

        # A. Calculate R: Sum of (r * Lambda(r) / Lambda(1))
        R = R + (current_r * current_lac) / lac_1

        # B. Calculate R_max: Sum of r (because Lambda(r) / Lambda(1) is 1 for homogeneous)
        R_max = R_max + current_r

    end

    # The standardization is R_scaled = R / R_max.
    # The final index h is inverted (1 - R_scaled) in the original paper.
    # HOWEVER, my R_max is already a sum of r, so the final calculation is simpler:
    # h = 1 - (R / R_max) where R is the *un-averaged* sum, and R_max is the *un-averaged* sum.

    h_scaled = R / R_max # This is the standardized measure (equivalent to R / R_max)

    # The Scott et al. (2022) paper's simplified formula applies when using the arithmetic series:
    # h = 1 - (2 * R / (N+1))
    # Since I use a discrete, power-of-two sampled R_max, I use the fundamental ratio:
    h = 1 - h_scaled
    
    return h

end
```

Next post, I will show how I combine this index with the **midpoint displacement algorithm** to explore the relation between lacunarity and fractal dimension. Stay tuned!