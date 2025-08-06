---
title: Part 4
layout: page
parent: Homework 3
nav_order: 4
---

# Part 4 – Global Illumination

## Description
In this part we extend the path tracer from direct illumination to **full global illumination**, allowing light to bounce multiple times and create effects such as colour bleeding and soft indirect shadows.  We implement cosine-weighted BSDF sampling, recursive multi-bounce radiance estimation, and Russian-Roulette termination to keep the estimator unbiased while maintaining efficiency.

## Implementation
The global-illumination code path required changes in three places:

1. **Diffuse sampling (`DiffuseBSDF::sample_f`)**  – replaced the stub with a cosine-weighted draw from the local hemisphere via `hemisphereSampler`.  The function:
   * fills `*wi` with the sampled direction;
   * sets `*pdf = cosθ/π` (zero if `cosθ ≤ 0`);
   * returns the constant BRDF value `ρ/π`.
   This ensures that directions closer to the surface normal, which contribute more to the integral, are sampled more often.

2. **Recursive estimator (`at_least_one_bounce_radiance`)**  – after adding the one-bounce term the routine:
   * samples an incoming direction `wi` from the BSDF;
   * spawns a secondary ray offset by `EPS_F` and with `depth--`;
   * multiplies the returned radiance by the BSDF, cosine term, and **Russian-Roulette weight** 
     `1 / (1−p_rr)` where `p_rr` is the termination probability (0.3).
   The recursion stops either when the ray misses the scene or when `depth == 0`.

3. **Top-level radiance (`est_radiance_global_illumination`)**  – now returns `zero_bounce + at_least_one_bounce`, giving complete lighting for diffuse scenes while still supporting debug modes used in earlier parts.

With these pieces the renderer can march paths of arbitrary length while remaining unbiased and reasonably fast.

## Results
### Global Illumination Examples  
(All renders use 1024 spp unless noted.)

| Scene | Direct only | Indirect only | Full GI |
|-------|-------------|---------------|---------|
| CBbunny | ![s](sphere_d.png) | ![s](spheres_ind.png) | ![s](spheres.png) |



### Per-bounce images (isAccumBounces = true)
 m = 1 | m = 2 | m = 3 | m = 4 | m = 5 |
-------|-------|-------|-------|-------|
| ![b1](bunnytm1.png) | ![b2](bunnytm2.png) | ![b3](bunnytm3.png) | ![b4](bunnytm4.png) | ![b5](bunnytm5.png) | 


### CBbunny with Russian Roulette rendering
| m=1 | m=2 | m=3 | m=4 | m=5 | m=100  |
|-------|-------------|---------------|---------|----------|------|
| ![b](Bunny1.png) | ![s](Bunny2.png) | ![s](Bunny3.png) | ![s](Bunny4.png) |![s](Bunny5.png) |![s](Bunny100.png)|

### Convergence with samples-per-pixel (CBspheres, 4 light rays)

| 1 | 2 | 4 | 8 | 16 | 64 | 1024 |
|---|---|---|---|----|----|------|
| ![s1](spheres1.png) | ![s2](spheres2.png) | ![s4](spheres4.png) | ![s8](spheres8.png) | ![s16](spheres16.png) | ![s64](spheres64.png) | ![s1024](spheres1024.png) |

## Analysis
**Indirect-lighting implementation.** The recursive estimator treats the rendering equation as a path integral: it adds the direct term, then randomly walks the path by sampling the diffuse BSDF.  Each step attenuates radiance by the BRDF, cosine, and the inverse of the Russian-Roulette survival probability; this keeps the estimator unbiased while adaptively shortening low-energy paths.

**Visual impact of higher bounces.** In the bounce-by-bounce images we observe that the first indirect bounce (m = 1) introduces strong colour bleeding—the red wall tints the bunny’s flank—while the second and third bounces add subtle ambient fills that lift the remaining shadows.  Beyond the third bounce contributions are barely perceptible, matching the diminishing energy predicted by theory.

**Accumulated vs. single-bounce views.** 
 Because only paths that exactly bounce 
m times contribute, higher-order terms are increasingly weak and diffuse—by the time you reach the 3rd or 4th bounce, almost every path has been absorbed or scattered away, so the image becomes very dark and uniformly gray.
Accumulated mode (isAccumBounces=true) sums all termsThe zero-bounce term gives self-emission, the first bounce adds crisp direct lighting and hard shadows, and the second bounce (first indirect) fills in deep shadows with soft, low-intensity light. By the third and fourth bounces, we can see smooth color bleeding and gently brightened corners.

**Russian Roulette effectiveness.** Depth-limited images show that as the m increases, the noise point would decreases but not totally disappear,(it might because we didn't use too much light rays).

**Sample convergence.** The spheres sequence demonstrates classic Monte-Carlo behaviour: doubling spp roughly halves the noise.  Notably, moving from 16→64 spp produces a visible improvement, while 64→1024 spp mainly polishes the last traces of grain—an important guideline for picking sample budgets in practice. 