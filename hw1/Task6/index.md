---
title: Task 6
layout: page
parent: Homework 1
nav_order: 6
---

# Task 6: "Level sampling" with mipmaps for texture mapping

## Overview

This task implements mipmap level sampling for texture mapping, supporting three level sampling methods: zero-level, nearest level, and linear level interpolation. The implementation enables adaptive texture resolution based on screen-space derivatives, significantly improving rendering quality and performance for textured surfaces.

## Implementation Details

### Approach

[**TODO: Explain level sampling in your own words and describe how you implemented it for texture mapping.**]

### Key Algorithms

- **Zero-Level Sampling**: Always sample from the highest resolution mipmap level
- **Nearest Level Sampling**: Compute and sample from the nearest appropriate mipmap level
- **Linear Level Sampling**: Interpolate between two adjacent mipmap levels
- **Derivative Calculation**: Compute texture coordinate derivatives for level selection
- **Trilinear Filtering**: Combination of bilinear pixel sampling and linear level sampling

### Code Structure

```cpp
// Key implementations in rasterizer.cpp and texture.cpp
void RasterizerImp::rasterize_textured_triangle(
    float x0, float y0, float u0, float v0,
    float x1, float y1, float u1, float v1,
    float x2, float y2, float u2, float v2,
    Texture& tex) {
    // TODO: Implement mipmap level sampling
    // 1. Calculate barycentric coordinates for (x,y), (x+1,y), (x,y+1)
    // 2. Compute texture coordinates for all three points
    // 3. Calculate derivatives du/dx, dv/dx, du/dy, dv/dy
    // 4. Create SampleParams struct and call Texture::sample
}

float Texture::get_level(const SampleParams& sp) {
    // TODO: Implement mipmap level calculation
    // 1. Calculate difference vectors sp.p_dx_uv - sp.p_uv and sp.p_dy_uv - sp.p_uv
    // 2. Scale by texture width and height
    // 3. Compute level using the formula from lecture
    // 4. Return appropriate mipmap level
}

Color Texture::sample(const SampleParams& sp) {
    // TODO: Implement level sampling with different methods
    // 1. Get mipmap level using get_level()
    // 2. Handle L_ZERO, L_NEAREST, L_LINEAR cases
    // 3. Call appropriate pixel sampling function
    // 4. For L_LINEAR, interpolate between two levels
}
```

## Mathematical Foundation

### Mipmap Level Calculation

The mipmap level is calculated using texture coordinate derivatives:

**Level = log₂(max(√(du/dx² + dv/dx²), √(du/dy² + dv/dy²)))**

where:

- du/dx, dv/dx are derivatives in x direction
- du/dy, dv/dy are derivatives in y direction

### Derivative Computation

[**TODO: Explain how you compute the texture coordinate derivatives**]

For a point (x,y) in screen space:

```
du/dx = u(x+1,y) - u(x,y)
dv/dx = v(x+1,y) - v(x,y)
du/dy = u(x,y+1) - u(x,y)
dv/dy = v(x,y+1) - v(x,y)
```

### Level Sampling Methods

[**TODO: Explain the three level sampling methods**]

1. **L_ZERO**: Always use level 0 (highest resolution)
2. **L_NEAREST**: Use the nearest integer level
3. **L_LINEAR**: Interpolate between two adjacent levels

## Results

### Sampling Method Comparisons

[**TODO: Using a png file you find yourself, show us four versions of the image, using the combinations of L_ZERO and P_NEAREST, L_ZERO and P_LINEAR, L_NEAREST and P_NEAREST, as well as L_NEAREST and P_LINEAR.**]

#### L_ZERO + P_NEAREST

![L_ZERO + P_NEAREST](L_zero_P_nearest.png)

#### L_ZERO + P_LINEAR

![L_ZERO + P_LINEAR](L_zero_P_linear.png)

#### L_NEAREST + P_NEAREST

![L_NEAREST + P_NEAREST](L_nearest_P_nearest.png)

#### L_NEAREST + P_LINEAR

![L_NEAREST + P_LINEAR](L_nearest_P_linear.png)

### Analysis

[**TODO: Discuss the visual differences and quality improvements**]

## Implementation Details

### SampleParams Structure

[**TODO: Explain how you use the SampleParams struct**]

```cpp
struct SampleParams {
    Vector2D p_uv;      // Texture coordinates at (x,y)
    Vector2D p_dx_uv;   // Texture coordinates at (x+1,y)
    Vector2D p_dy_uv;   // Texture coordinates at (x,y+1)
    // ... other parameters
};
```

### Derivative Calculation

[**TODO: Explain your approach to computing texture coordinate derivatives**]

### Level Interpolation

[**TODO: Explain how you implement linear level sampling**]

## Performance and Quality Tradeoffs

[**TODO: Describe the tradeoffs between speed, memory usage, and antialiasing power between the three various techniques.**]

### Comparison Table

| Method                          | Quality | Performance | Memory Usage | Antialiasing Power |
| ------------------------------- | ------- | ----------- | ------------ | ------------------ |
| L_ZERO + P_NEAREST              | [TODO]  | [TODO]      | [TODO]       | [TODO]             |
| L_ZERO + P_LINEAR               | [TODO]  | [TODO]      | [TODO]       | [TODO]             |
| L_NEAREST + P_NEAREST           | [TODO]  | [TODO]      | [TODO]       | [TODO]             |
| L_NEAREST + P_LINEAR            | [TODO]  | [TODO]      | [TODO]       | [TODO]             |
| L_LINEAR + P_LINEAR (Trilinear) | [TODO]  | [TODO]      | [TODO]       | [TODO]             |

## Challenges and Solutions

### Challenges Faced

- **Derivative Calculation**: Computing accurate texture coordinate derivatives
- **Level Selection**: Determining the appropriate mipmap level
- **Level Interpolation**: Smoothly interpolating between mipmap levels
- **Performance Optimization**: Avoiding unnecessary mipmap copies

### Solutions Implemented

- **Derivative Computation**: [**TODO: Explain your derivative calculation approach**]
- **Level Calculation**: [**TODO: Explain your mipmap level selection**]
- **Interpolation Method**: [**TODO: Explain your level interpolation**]
- **Memory Management**: [**TODO: Explain how you avoid copying miplevels**]

## Mipmap Visualization

### Level Debugging

[**TODO: Explain how you used level visualization for debugging**]

You can visualize mipmap levels by normalizing the level value and using it as a color:

```
Color debug_color = Color(level/max_level, level/max_level, level/max_level);
```

### Zoom Effects

[**TODO: Show examples of how mipmap levels change with zoom**]

## Extra Credit: Advanced Filtering

[**TODO: If you implemented extra credit, describe anisotropic filtering or summed area tables**]

### Method Description

[**TODO: Explain your advanced filtering method**]

### Performance Comparison

| Method          | Quality | Performance | Memory Usage |
| --------------- | ------- | ----------- | ------------ |
| Nearest         | [TODO]  | [TODO]      | [TODO]       |
| Bilinear        | [TODO]  | [TODO]      | [TODO]       |
| Trilinear       | [TODO]  | [TODO]      | [TODO]       |
| Advanced Method | [TODO]  | [TODO]      | [TODO]       |

### Comparison Images

[**TODO: Show comparison images demonstrating the differences**]

## Testing

### Test Files

- Custom PNG texture files
- Modified SVG files from `svg/texmap/`
- Various zoom levels and viewing angles

### Verification

[**TODO: Explain how you verified your mipmap implementation works correctly**]

## Integration with Previous Tasks

### Building on Task 5

[**TODO: Discuss how this extends the texture mapping from Task 5**]

### Complete Pipeline

[**TODO: Explain how all tasks work together in the final rendering pipeline**]

## Conclusion

[**TODO: Summary of what was learned about mipmaps and level sampling**]

## Additional Examples

[**TODO: Include any additional test cases or interesting mipmap effects**]

### Custom Textures

[**TODO: Show additional examples with different textures**]

![Additional Examples](additional_mipmaps.png)
