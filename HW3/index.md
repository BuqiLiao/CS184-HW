---
title: Homework 3
layout: page
nav_order: 3
has_children: true
---

# Homework 3: Path Tracer

This assignment builds a physically based Monte-Carlo path tracer in five incremental parts, transforming a bare‐bones ray caster into a renderer that supports global illumination and adaptive sampling.

## Parts

1. [Part 1 – Ray Generation & Scene Intersection](part1/)  
   Generate camera rays, implement pixel sampling, and add ray–triangle/sphere intersection tests.
2. [Part 2 – Bounding Volume Hierarchy](part2/)  
   Accelerate ray queries with a hierarchical BVH, reducing intersection cost from **O(n)** to **O(log n)**.
3. [Part 3 – Direct Illumination](part3/)  
   Add diffuse BSDFs and two estimators for direct lighting: uniform-hemisphere and light-importance sampling.
4. [Part 4 – Global Illumination](part4/)  
   Extend the integrator to multiple bounces, implement Russian Roulette, and render full colour bleeding.
5. [Part 5 – Adaptive Sampling](part5/)  
   Use per-pixel variance estimates to stop sampling early where the image has already converged.

## Acknowledgement of AI

AI used in the homework: GPT 5.
I used it in debugging Task 2 in part 4 where I have a small error on the 'at_least_one_bounce_radiance' when calculating the light bounces; Also, I use AI to generate some test cases and debugging information, eg. (print out the messages of the light reflected numbers when rendering).
