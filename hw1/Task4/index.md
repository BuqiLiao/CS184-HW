---
title: Task 4
layout: page
parent: Homework 1
nav_order: 4
---

# Task 4: Barycentric Coordinates

## Overview

This task implements barycentric coordinate interpolation for triangles, allowing smooth color blending across triangle surfaces. The implementation enables rendering triangles with colors defined at vertices and interpolated across the entire triangle area, creating smooth gradients and color transitions.

## Implementation Details

### Approach

[**TODO: Explain your approach to implementing barycentric coordinate interpolation**]

### Key Algorithms

- **Barycentric Coordinate Calculation**: Computing (α, β, γ) coordinates for each pixel
- **Color Interpolation**: Linear interpolation of vertex colors using barycentric weights
- **Point-in-Triangle Test**: Using barycentric coordinates for inside/outside testing
- **Smooth Blending**: Ensuring continuous color transitions across triangle boundaries

### Code Structure

```cpp
// Key implementation in rasterizer.cpp
void RasterizerImp::rasterize_interpolated_color_triangle(
    float x0, float y0, Color c0,
    float x1, float y1, Color c1,
    float x2, float y2, Color c2) {
    // TODO: Implement barycentric interpolation
    // 1. Calculate barycentric coordinates for each pixel
    // 2. Test if pixel is inside triangle using barycentric coordinates
    // 3. Interpolate colors using barycentric weights
    // 4. Fill pixel with interpolated color
}
```

## Mathematical Foundation

### Barycentric Coordinates

[**TODO: Explain barycentric coordinates in your own words and use an image to aid you in your explanation. One idea is to use a svg file that plots a single triangle with one red, one green, and one blue vertex, which should produce a smoothly blended color triangle.**]

Barycentric coordinates (α, β, γ) represent a point P inside a triangle as a weighted combination of the three vertices:

**P = αA + βB + γC**

where:

- α + β + γ = 1
- α, β, γ ≥ 0 (for points inside the triangle)

### Color Interpolation

The interpolated color at point P is:

**C(P) = αC(A) + βC(B) + γC(C)**

where C(A), C(B), C(C) are the colors at vertices A, B, and C respectively.

### Barycentric Coordinate Calculation

[**TODO: Show the mathematical formulas for computing barycentric coordinates**]

For a triangle with vertices A(x₀,y₀), B(x₁,y₁), C(x₂,y₂) and point P(x,y):

```
α = ((y₁-y₂)(x-x₂) + (x₂-x₁)(y-y₂)) / ((y₁-y₂)(x₀-x₂) + (x₂-x₁)(y₀-y₂))
β = ((y₂-y₀)(x-x₂) + (x₀-x₂)(y-y₂)) / ((y₁-y₂)(x₀-x₂) + (x₂-x₁)(y₀-y₂))
γ = 1 - α - β
```

## Results

### Color Wheel (test7.svg)

[**TODO: Show a png screenshot of svg/basic/test7.svg with default viewing parameters and sample rate 1**]

![Color Wheel](test7_color_wheel.png)

### RGB Triangle Example

[**TODO: If you make any additional images with color gradients, include them**]

![RGB Triangle](rgb_triangle.png)

### Analysis

[**TODO: Discuss the smoothness of color transitions, interpolation quality, and any artifacts**]

## Implementation Details

### Barycentric Coordinate Computation

[**TODO: Explain your implementation of barycentric coordinate calculation**]

### Color Interpolation Algorithm

[**TODO: Explain how you interpolate colors using barycentric weights**]

### Edge Cases and Precision

[**TODO: Discuss handling of edge cases and numerical precision issues**]

## Challenges and Solutions

### Challenges Faced

- **Numerical Precision**: Avoiding division by zero and floating-point errors
- **Edge Handling**: Ensuring smooth color transitions at triangle edges
- **Coordinate Calculation**: Efficient computation of barycentric coordinates
- **Color Space**: Proper interpolation in RGB color space

### Solutions Implemented

- **Robust Division**: [**TODO: Explain your approach to avoiding division by zero**]
- **Edge Smoothing**: [**TODO: Explain how you handle edge cases**]
- **Efficient Computation**: [**TODO: Explain optimizations in coordinate calculation**]
- **Color Handling**: [**TODO: Explain your color interpolation approach**]

## Performance Considerations

### Computational Complexity

[**TODO: Analyze the performance impact of barycentric coordinate calculation**]

### Optimization Strategies

[**TODO: Discuss any optimizations you implemented**]

## Testing

### Test Files

- `svg/basic/test7.svg` - Color wheel demonstration
- Custom RGB triangle for barycentric coordinate visualization

### Verification

[**TODO: Explain how you verified your barycentric interpolation works correctly**]

## Comparison with Previous Tasks

### Differences from Task 1

[**TODO: Compare with single-color triangle rasterization**]

### Integration with Task 2

[**TODO: Discuss how supersampling affects color interpolation**]

## Conclusion

[**TODO: Summary of what was learned about barycentric coordinates and color interpolation**]

## Additional Examples

[**TODO: Include any additional test cases or interesting color gradients you created**]

### Custom Color Gradients

[**TODO: Show additional examples of color interpolation**]

![Additional Examples](additional_gradients.png)
