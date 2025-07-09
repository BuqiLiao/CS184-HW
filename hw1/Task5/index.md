---
title: Task 5
layout: page
parent: Homework 1
nav_order: 5
---

# Task 5: "Pixel sampling" for texture mapping

## Overview

This task implements texture mapping for triangles using two pixel sampling methods: nearest neighbor and bilinear interpolation. The implementation enables rendering triangles with colors sampled from texture images using 2D texture coordinates, providing realistic surface detail and patterns.

## Implementation Details

### Approach

Pixel sampling is the process of determining the color value at a specific texture coordinate (u,v) by sampling from the texture image. I implemented texture mapping by interpolating texture coordinates using barycentric coordinates and then sampling the texture using either nearest neighbor or bilinear interpolation methods.

**Nearest Neighbor Sampling**: Selects the closest texel to the sample point by rounding the texture coordinates to the nearest integer texel position. This method is fast but can produce aliasing artifacts, especially when the texture is magnified.

**Bilinear Interpolation**: Computes a weighted average of the four nearest texels using linear interpolation in both u and v directions. This method provides smoother results and reduces aliasing, but requires more computation.

### Key Algorithms

- **Nearest Neighbor Sampling**: Select the closest texel to the sample point
- **Bilinear Interpolation**: Weighted average of four nearest texels
- **Texture Coordinate Interpolation**: Using barycentric coordinates to interpolate UV coordinates
- **Mipmap Level 0**: Using full-resolution texture for sampling

### Code Structure

- `sample_nearest` and `sample_bilinear` functions in `texture.cpp`
- `rasterize_textured_triangle` function in `rasterizer.cpp`

### Texture Coordinate Handling

Texture coordinates are interpolated using barycentric coordinates in the `rasterize_textured_triangle` function:

```cpp
// Interpolate texture coordinates using barycentric weights
float u = alpha * u0 + beta * u1 + gamma * u2;
float v = alpha * v0 + beta * v1 + gamma * v2;
```

This ensures smooth texture coordinate interpolation across the triangle surface, maintaining perspective correctness.

### Sampling Method Selection

The sampling method is selected through the `SampleParams` structure:

```cpp
SampleParams sp;
sp.psm = psm;  // P_NEAREST or P_LINEAR
sp.lsm = lsm;  // Level sampling method (For task 6)
sp.p_uv = Vector2D(u, v);
```

The `sample()` function then dispatches to the appropriate sampling method based on `sp.psm`.

## Mathematical Foundation

### Texture Coordinate Interpolation

Texture coordinates (u,v) are interpolated using barycentric coordinates:

**u(P) = αu₀ + βu₁ + γu₂**
**v(P) = αv₀ + βv₁ + γv₂**

where (u₀,v₀), (u₁,v₁), (u₂,v₂) are texture coordinates at vertices.

### Nearest Neighbor Sampling

For texture coordinates (u,v), the nearest texel is determined by:

1. **Coordinate Clamping**: Clamp u and v to [0,1] range
2. **Texel Mapping**: Convert to texel coordinates using floor function
3. **Boundary Clamping**: Ensure texel coordinates are within texture bounds

```
// Clamp UV coordinates to [0,1]
u = clamp(u, 0, 1)
v = clamp(v, 0, 1)

// Convert to integer texel coordinates
texel_x = floor(u * texture_width)
texel_y = floor(v * texture_height)

// Clamp to valid texture bounds
texel_x = clamp(texel_x, 0, texture_width - 1)
texel_y = clamp(texel_y, 0, texture_height - 1)
```

The implementation uses `std::floor()` to get the integer texel coordinates and then clamps them to valid texture bounds using `std::min()` and `std::max()`.

### Bilinear Interpolation

For texture coordinates (u,v), bilinear interpolation computes a weighted average of four surrounding texels:

1. **Coordinate Mapping**: Map UV coordinates to texture space using `(width-1)` and `(height-1)` scaling
2. **Four-Texel Selection**: Identify the four nearest texels (x0,y0), (x1,y0), (x0,y1), (x1,y1)
3. **Interpolation Weights**: Compute fractional parts sx and sy from the continuous texture coordinates
4. **Two-Step Interpolation**: First interpolate horizontally between (x0,y0)-(x1,y0) and (x0,y1)-(x1,y1), then vertically

```
// Texture space mapping
x = u * (width - 1)
y = v * (height - 1)

// Texel coordinates
x0 = floor(x), y0 = floor(y)
x1 = min(x0 + 1, width - 1), y1 = min(y0 + 1, height - 1)

// Interpolation weights
sx = x - x0, sy = y - y0

// Two-step interpolation
c0 = lerp(c00, c10, sx)  // Horizontal interpolation at y0
c1 = lerp(c01, c11, sx)  // Horizontal interpolation at y1
c = lerp(c0, c1, sy)     // Vertical interpolation
```

where sx and sy are the fractional parts of the continuous texture coordinates.

## Results

### Comparison Screenshots

The following screenshots demonstrate the difference between nearest neighbor and bilinear sampling methods. The test uses a texture with fine details to clearly show the quality differences.

#### Nearest Sampling - 1 Sample per Pixel

![Nearest 1x](nearest_1x.png)

#### Nearest Sampling - 16 Samples per Pixel

![Nearest 16x](nearest_16x.png)

#### Bilinear Sampling - 1 Sample per Pixel

![Bilinear 1x](bilinear_1x.png)

#### Bilinear Sampling - 16 Samples per Pixel

![Bilinear 16x](bilinear_16x.png)

### Analysis

**Nearest Neighbor Sampling**: Shows clear pixelation and aliasing artifacts, especially visible as jagged edges and blocky patterns. The 16x supersampling helps reduce some aliasing but the fundamental blocky nature remains.

**Bilinear Sampling**: Produces much smoother results with reduced aliasing. The interpolation between texels creates gradual color transitions, eliminating the sharp pixel boundaries seen in nearest neighbor sampling.

**Key Differences**: The largest differences occur when:

1. **Texture Magnification**: When a small texture is stretched over a large area
2. **Diagonal Patterns**: When texture contains diagonal lines or patterns
3. **High-Frequency Details**: When texture contains fine details or sharp edges

Bilinear sampling shows clear advantages in these scenarios because it smooths out the discrete texel boundaries.

## Performance Considerations

### Sampling Method Comparison

| Method           | Quality | Performance | Memory Access |
| ---------------- | ------- | ----------- | ------------- |
| Nearest Neighbor | Low     | High        | 1 texel       |
| Bilinear         | High    | Medium      | 4 texels      |

## Testing

### Test Files

- `svg/texmap/test1.svg`
- `svg/texmap/test2.svg`
- `svg/texmap/test4.svg`
- `svg/texmap/test5.svg`
- `svg/texmap/test6.svg`
