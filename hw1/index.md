---
title: Homework 1
layout: page
nav_order: 1
has_children: true
---

# Homework 1: Rasterization and Basic Rendering

## Overview

This homework assignment covers fundamental concepts in computer graphics and rasterization. The assignment is divided into 6 tasks, each focusing on different aspects of the rendering pipeline, from basic triangle rasterization to advanced texture mapping with mipmaps.

## Tasks

### [Task 1](Task1/)

**Drawing Single-Color Triangles**

Implement triangle rasterization using point-in-triangle tests with pixel center sampling. The implementation handles triangles regardless of winding order and efficiently samples within the triangle's bounding box.

### [Task 2](Task2/)

**Antialiasing by Supersampling**

Implement supersampling antialiasing by sampling multiple times per pixel and averaging results. The implementation uses a higher-resolution sample buffer and downsamples to the final framebuffer resolution.

### [Task 3](Task3/)

**Transforms**

Implement geometric transformations (translate, scale, rotate) in homogeneous coordinates using 3×3 matrices. These transforms enable hierarchical transformations of SVG objects for complex animations and positioning.

### [Task 4](Task4/)

**Barycentric Coordinates**

Implement barycentric coordinate interpolation for triangles, allowing smooth color blending across triangle surfaces. Colors defined at vertices are interpolated across the entire triangle area.

### [Task 5](Task5/)

**Pixel Sampling for Texture Mapping**

Implement texture mapping using two pixel sampling methods: nearest neighbor and bilinear interpolation. The implementation enables rendering triangles with colors sampled from texture images using 2D texture coordinates.

### [Task 6](Task6/)

**Level Sampling with Mipmaps**

Implement mipmap level sampling for texture mapping, supporting three level sampling methods: zero-level, nearest level, and linear level interpolation. This enables adaptive texture resolution based on screen-space derivatives.

## Learning Objectives

- **Triangle Rasterization**: Understand and implement efficient triangle filling algorithms
- **Antialiasing Techniques**: Learn supersampling methods for reducing visual artifacts
- **Geometric Transformations**: Master homogeneous coordinates and matrix transformations
- **Color Interpolation**: Implement smooth color blending using barycentric coordinates
- **Texture Mapping**: Understand texture sampling and filtering techniques
- **Mipmap Filtering**: Learn adaptive texture resolution for quality and performance

## Technologies Used

- **C++**: Core implementation language
- **OpenGL**: Graphics API for rendering
- **CMake**: Build system configuration
- **Jekyll**: Documentation website generation
- **SVG**: Vector graphics format for test cases
- **PNG**: Image format for texture mapping

## Key Concepts Covered

### Rasterization Pipeline

1. **Triangle Setup**: Bounding box calculation and edge function computation
2. **Sampling**: Point-in-triangle tests with pixel center sampling
3. **Antialiasing**: Supersampling and downsampling techniques
4. **Transformation**: Hierarchical geometric transformations
5. **Interpolation**: Barycentric coordinate-based color and texture interpolation
6. **Texture Mapping**: UV coordinate interpolation and texture sampling
7. **Mipmap Filtering**: Adaptive texture resolution selection

### Performance Considerations

- **Bounding Box Optimization**: Efficient sampling within triangle bounds
- **Memory Management**: Dynamic buffer sizing for supersampling
- **Sampling Quality**: Trade-offs between nearest neighbor and bilinear filtering
- **Level Selection**: Adaptive mipmap level based on screen-space derivatives

## Submission Requirements

- All 6 tasks must be completed and documented
- Code should be well-commented and organized
- Results should be clearly presented with comparison images
- Performance analysis should be included where relevant
- Screenshots must be generated using the 'S' hotkey in the GUI
- Custom examples and demonstrations are encouraged

## Resources

- **Course Materials**: CS184 Lecture Notes (Lectures 2-5)
- **Test Files**: SVG files in `svg/basic/`, `svg/transforms/`, and `svg/texmap/` directories
- **Reference**: OpenGL documentation and graphics programming guides
- **GUI Controls**: Use 'P' for pixel sampling, 'L' for level sampling, '-/=' for sample rate
