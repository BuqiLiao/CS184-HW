---
title: Part 1 – Ray Generation and Scene Intersection
layout: page
parent: Homework 3
nav_order: 1
---

# Part 1 – Ray Generation & Scene Intersection

This section builds the full pipeline that takes us **from pixels to geometry**:
1. Map 2-D pixel coordinates onto the virtual film plane in camera space (**Task 1**).
2. Generate multiple random samples per pixel and estimate radiance (**Task 2**).
3. Test the intersection between a ray and a triangle (**Task 3**).
4. Test the intersection between a ray and a sphere (**Task 4**).

With these pieces in place the renderer can already visualise camera-ray directions, surface normals and basic occlusion, laying the groundwork for global-illumination algorithms in later parts.

---
## Task 1 – Generating Camera Rays


Construct a ray $(o_c,\,d_c)$ whose origin is the camera $(0,0,0)$ and whose direction points at the mapped film-plane position. Normalise the direction and transform it to world space using the rotation matrix `c2w` and translation `pos`, yielding $(o_w,\,d_w)$. Finally set
`ray.min_t = nClip`, `ray.max_t = fClip`.


### Result
Visualising the world-space ray direction for each pixel (RGB ← XYZ):

<p float="left">
  <img src="CBempty.png" alt="empty" width="350"/>
  <img src="banana.png" alt="banana" width="350"/>
</p>

---
## Task 2 – Generating Pixel Samples
### Idea
For each pixel $(i,\,j)$:
1. Draw `ns_aa` random samples $(u,v)$ in $[0,1]^2$ using `gridSampler`.
2. Convert $(i+u,\,j+v)$ to normalised image space $(x,y)\in[0,1]^2$ and call `camera->generate_ray()`.
3. Estimate radiance along that ray via `est_radiance_global_illumination(ray)` and accumulate.
4. Write the average to `sampleBuffer`.

### Key Implementation
`src/pathtracer/pathtracer.cpp`
```cpp
void PathTracer::raytrace_pixel(size_t x, size_t y) {
    Vector3D L(0);
    for (int s = 0; s < ns_aa; ++s) {
        Vector2D sample = gridSampler->get_sample();
        double nx = (x + sample.x) / sampleBuffer.w;
        double ny = (y + sample.y) / sampleBuffer.h;
        Ray r = camera->generate_ray(nx, ny);
        L += est_radiance_global_illumination(r);
    }
    L /= (double)ns_aa;
    sampleBuffer.update_pixel(L, x, y);
}
```

### Result
Ray-direction visualisation with multiple random samples:

![CBempty2](CBempty2.png)

---
## Task 3 – Ray–Triangle Intersection
### Algorithm (Möller–Trumbore)
1. Let the triangle vertices be $p_1, p_2, p_3$ and the ray $o + t\,d$.
2. $e_1 = p_2 - p_1$, $e_2 = p_3 - p_1$, $h = d \times e_2$, $a = e_1 \cdot h$.  If $|a| < \varepsilon$ the ray is parallel.
3. $f = 1/a$, $s = o - p_1$, $u = f\,(s \cdot h)$; reject if $u\notin[0,1]$.
4. $q = s \times e_1$, $v = f\,(d \cdot q)$; reject if $v<0$ or $u+v>1$.
5. $t = f\,(e_2 \cdot q)$; accept if $t \in [\text{min\_t}, \text{max\_t}]$.
6. Interpolate the vertex normals using barycentric coords $(1-u-v,u,v)$, update `ray.max_t` and fill the `Intersection` record.

### Result
The correct surface normals become visible after this step:

![CBempty2](CBempty2.png)

---
## Task 4 – Ray–Sphere Intersection
### Algorithm
Insert the ray into the sphere equation $\|p-c\|^2 = r^2$ to obtain
$$ (d\cdot d)\,t^2 + 2d\cdot(o-c)\,t + \|o-c\|^2 - r^2 = 0. $$
Solve for $t_{0,1}$, choose the smallest positive $t$ within $[\text{min\_t},\text{max\_t}]$, update `ray.max_t` and compute the normal $(p-c)/r$.

### Result
![CBspheres](CBspheres.png)

---
## Write-Up

The **ray-generation and primitive-intersection pipeline** begins by jitter-sampling each pixel and translating the jittered coordinates into the unit square.  For every sample the camera maps the 2-D position onto its virtual film plane, builds a world-space ray, and initialises its valid interval with the near/far clip distances.  The path-tracer sends this ray into the scene where each geometric primitive is asked whether it lies within the ray’s current `min_t‥max_t` range.  Whenever a hit is found the ray’s `max_t` is shortened to that distance so only nearer intersections remain eligible, guaranteeing that after all tests the first visible surface along the view direction is reported.  The intersection record returned contains the hit point, interpolated normal, material pointer and the refined `t`, which downstream shading code will use to evaluate lighting.

The **triangle intersection test** is implemented with the classic *Möller–Trumbore* algorithm.  we treat one triangle edge pair as a local basis and express the candidate hit point in barycentric coordinates.  By crossing the ray direction with one edge I build a helper vector whose dot-product with the second edge yields the reciprocal determinant `1/a`.  Multiplying that reciprocal with a handful of additional dot and cross products gives the barycentric weights `u`, `v` and the distance `t` in one tight expression chain—no matrix inverses required.  The test therefore boils down to five vector products and a few comparisons: `u≥0`, `v≥0`, `u+v≤1` for inside-triangle containment and `t` within the ray’s clip range.  When all conditions pass I interpolate the three per-vertex normals using `(1-u-v, u, v)`, update `ray.max_t` to `t`, and store the result in the `Intersection` structure.
