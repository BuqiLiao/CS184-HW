---
title: Task 1
layout: page
parent: Homework 1
nav_order: 1
---

# Task 1: Drawing Single-Color Triangles

## Overview

This task implements the `rasterize_triangle` function in `rasterizer.cpp` to draw single-color triangles using point-in-triangle tests with sample points at pixel centers. The implementation must handle triangles regardless of winding order and efficiently rasterize within the triangle's bounding box.

## Implementation Details

### Approach

[**TODO: Walk through how you rasterize triangles in your own words**]

### Key Algorithms

- **Point-in-Triangle Test**: Using barycentric coordinates or edge function tests
- **Bounding Box Optimization**: Sampling only within the triangle's bounding box
- **Pixel Center Sampling**: Sample point at (x+0.5, y+0.5) for each pixel

### Code Structure

```cpp
// Key implementation in rasterizer.cpp
void RasterizerImp::rasterize_triangle(float x0, float y0, float x1, float y1, float x2, float y2, Color color) {
    // TODO: Add your implementation here
    // 1. Calculate bounding box
    // 2. For each pixel in bounding box
    // 3. Test if pixel center is inside triangle
    // 4. If inside, call fill_pixel()
}
```

## Results

### Output Images

[**TODO: Show a png screenshot of basic/test4.svg with the default viewing parameters and with the pixel inspector centered on an interesting part of the scene**]

![Task 1 Result - test4.svg](test4_result.png)

### Analysis

[**TODO: Discuss the results and any observations about triangle rendering quality, edge handling, etc.**]

## Algorithm Efficiency

[**TODO: Explain how your algorithm is no worse than one that checks each sample within the bounding box of the triangle**]

The bounding box of the triangle is defined as the smallest rectangle that can be drawn whilst ensuring that the entire triangle is within it.

## Challenges and Solutions

### Challenges Faced

- **Winding Order**: Triangles can be defined in clockwise or counter-clockwise order
- **Edge Cases**: Handling samples exactly on triangle edges
- **Efficiency**: Avoiding checking every pixel in the framebuffer

### Solutions Implemented

- **Winding Order Independence**: [**TODO: Explain how you handle different winding orders**]
- **Edge Handling**: [**TODO: Explain your approach to edge cases**]
- **Bounding Box Optimization**: [**TODO: Explain your bounding box implementation**]

## Performance Considerations

### Basic Implementation

[**TODO: Discuss the performance characteristics of your basic implementation**]

### Extra Credit Optimizations

[**TODO: If you implemented extra credit optimizations, explain them here with timing comparisons**]

| Implementation | Time (ms) | Optimization Details           |
| -------------- | --------- | ------------------------------ |
| Basic          | [TODO]    | Standard bounding box approach |
| Optimized      | [TODO]    | [TODO: List optimizations]     |

## Conclusion

[**TODO: Summary of what was learned and accomplished in this task**]

## Testing

The implementation successfully renders the following test files:

- `basic/test3.svg`
- `basic/test4.svg`
- `basic/test5.svg`
- `basic/test6.svg` (tests winding order independence)
