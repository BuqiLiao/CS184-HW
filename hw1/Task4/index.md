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


- **Barycentric Coordinate Calculation**: Computing (α, β, γ) coordinates for each pixel
- **Color Interpolation**: Linear interpolation of vertex colors using barycentric weights
- **Point-in-Triangle Test**: Using barycentric coordinates for inside/outside testing
- **Smooth Blending**: Ensuring continuous color transitions across triangle boundaries



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


For a triangle with vertices A(x₀,y₀), B(x₁,y₁), C(x₂,y₂) and point P(x,y):

```
α = ((y₁-y₂)(x-x₂) + (x₂-x₁)(y-y₂)) / ((y₁-y₂)(x₀-x₂) + (x₂-x₁)(y₀-y₂))
β = ((y₂-y₀)(x-x₂) + (x₀-x₂)(y-y₂)) / ((y₁-y₂)(x₀-x₂) + (x₂-x₁)(y₀-y₂))
γ = 1 - α - β
```

## Results


![Color Wheel](test7_color_wheel.png)


![RGB Triangle](rgb_triangle.png)

## Implementation Details


## Testing

### Test Files

- `svg/basic/test7.svg` - Color wheel demonstration
- Custom RGB triangle for barycentric coordinate visualization



## Comparison with Previous Tasks

