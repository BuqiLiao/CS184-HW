---
title: Task 1
layout: page
parent: Homework 2
nav_order: 1
---

# Task 1: Bezier Curves with 1D de Casteljau Subdivision

## Overview

This task implements 1D de Casteljau subdivision for Bezier curves. 

## Implementation
De Casteljau’s algorithm evaluate Bézier curves at a parameter t by repeated linear interpolation of the control points:P0 to Pn. In the single step, we take all the current points as an input and compute new interpolated points by using the formula(1-t)p<sub>i</sub>+ tp<sub>i+1</sub>. So by repeating the step recursively, we can get interpolated points until only one point left.

## Screenshots
![step 1](1.png)
![step 2](2.png)
![step 3](3.png)
![step 4](4.png)
![step 5](5.png)
![step 6](6.png)
![different t](7.png)
