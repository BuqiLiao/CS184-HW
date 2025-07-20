---
title: Homework 2
layout: page
nav_order: 2
has_children: true
---

# Homework 2: Bezier Curves, Surfaces and Mesh Operations

## Overview

This homework assignment covers fundamental concepts in geometric modeling and mesh processing. The assignment is divided into 6 parts, exploring Bezier curves and surfaces using de Casteljau algorithm, and implementing various mesh operations using the half-edge data structure.

## Tasks

### [Task 1](Task1/)

**Bezier Curves with 1D de Casteljau Subdivision**

Implement the de Casteljau algorithm to evaluate Bezier curves. The algorithm uses recursive linear interpolation to compute points on a Bezier curve defined by control points.

### [Task 2](Task2/)

**Bezier Surfaces with Separable 1D de Casteljau**

Extend the Bezier curve implementation to Bezier surfaces using separable 1D de Casteljau algorithm. This involves evaluating curves along u and v parameters to generate smooth surfaces.

### [Task 3](Task3/)

**Area-Weighted Vertex Normals**

Implement area-weighted normal vectors at vertices for improved shading. This enables Phong shading which provides smoother surface rendering compared to flat shading.

### [Task 4](Task4/)

**Edge Flip**

Implement local remeshing operation that flips edges between adjacent triangles. This operation maintains mesh topology while changing the connectivity of triangles.

### [Task 5](Task5/)

**Edge Split**

Implement edge splitting operation that inserts a new vertex at the edge midpoint and creates additional triangles. This operation increases mesh resolution locally.

### [Task 6](Task6/)

**Loop Subdivision for Mesh Upsampling**

Implement loop subdivision algorithm to upsample coarse meshes into higher-resolution ones. This involves subdividing triangles and updating vertex positions using weighted averages.
