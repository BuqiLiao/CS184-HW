---
title: Task 3
layout: page
parent: Homework 1
nav_order: 3
---

# Task 3: Transforms

## Overview

This task implements three fundamental geometric transformations (translate, scale, rotate) in homogeneous coordinates using 3×3 matrices. These transforms enable hierarchical transformations of SVG objects, allowing for complex animations and positioning of graphical elements.

## Implementation Details

### Approach

[**TODO: Explain your approach to implementing the three transforms in homogeneous coordinates**]

### Key Algorithms

- **Translation Matrix**: Move objects by specified x and y offsets
- **Scaling Matrix**: Scale objects by specified x and y factors
- **Rotation Matrix**: Rotate objects by specified angle around origin
- **Homogeneous Coordinates**: Using 3×3 matrices for 2D transformations

### Code Structure

```cpp
// Key implementations in transforms.cpp
Matrix3x3 translate(float dx, float dy) {
    // TODO: Implement translation matrix
    // Returns 3x3 matrix that translates by (dx, dy)
}

Matrix3x3 scale(float sx, float sy) {
    // TODO: Implement scaling matrix
    // Returns 3x3 matrix that scales by (sx, sy)
}

Matrix3x3 rotate(float deg) {
    // TODO: Implement rotation matrix
    // Returns 3x3 matrix that rotates by deg degrees
    // Note: deg is in degrees, convert to radians for sin/cos
}
```

## Results

### Original Robot

[**TODO: Show screenshot of the original svg/transforms/robot.svg rendering correctly**]

![Original Robot](robot_original.png)

### Custom Robot Animation

[**TODO: Create an updated version of svg/transforms/robot.svg with cubeman doing something more interesting, like waving or running. Save your svg file as my_robot.svg in your docs/ directory and show a png screenshot of your rendered drawing. Explain what you were trying to do with cubeman in words.**]

![Custom Robot Animation](my_robot.png)

### Animation Description

[**TODO: Explain what you were trying to do with cubeman - describe the animation, poses, or actions you created**]

## Mathematical Foundation

### Homogeneous Coordinates

[**TODO: Explain why we use 3x3 matrices for 2D transformations**]

### Transformation Matrices

[**TODO: Show the mathematical form of each transformation matrix**]

#### Translation Matrix

```
[ 1  0  dx ]
[ 0  1  dy ]
[ 0  0   1 ]
```

#### Scaling Matrix

```
[ sx  0   0 ]
[  0  sy  0 ]
[  0  0   1 ]
```

#### Rotation Matrix

```
[ cos(θ)  -sin(θ)  0 ]
[ sin(θ)   cos(θ)  0 ]
[   0       0      1 ]
```

## Implementation Details

### Matrix Operations

[**TODO: Explain how the * operator works with Vector2D and Matrix3x3**]

### Hierarchical Transforms

[**TODO: Explain how nested <g> elements with transforms work**]

Example SVG structure:

```xml
<g transform="rotate(135)">
  <g transform="translate(10, 20)">
    <g transform="scale(2, 1)">
      <!-- polygon definitions -->
    </g>
  </g>
</g>
```

## Challenges and Solutions

### Challenges Faced

- **Angle Conversion**: Converting between degrees and radians
- **Matrix Multiplication**: Ensuring correct order of transformations
- **Hierarchical Transforms**: Understanding how nested transforms combine
- **Coordinate Systems**: Working with homogeneous coordinates

### Solutions Implemented

- **Angle Handling**: [**TODO: Explain your approach to angle conversion**]
- **Matrix Implementation**: [**TODO: Explain your matrix construction**]
- **Transform Composition**: [**TODO: Explain how transforms combine**]
- **Testing Strategy**: [**TODO: Explain how you tested your transforms**]

## Extra Credit: GUI Enhancement

[**TODO: If you implemented extra credit, describe your GUI feature and show example images**]

### Feature Description

[**TODO: Describe the extra GUI feature you added**]

### Implementation Details

[**TODO: Explain how you modified the SVG to NDC and NDC to screen-space matrix stack**]

### Example Image

![Extra Credit Feature](extra_credit_demo.png)

## Testing

### Test Files

- `svg/transforms/robot.svg` - Basic transform testing
- `my_robot.svg` - Custom animation demonstration

### Verification

[**TODO: Explain how you verified your transforms work correctly**]

## Conclusion

[**TODO: Summary of what was learned about geometric transformations and homogeneous coordinates**]

## SVG File: my_robot.svg

[**TODO: Include your custom robot SVG file content or reference to the file**]

```xml
<!-- TODO: Show your custom robot SVG code or reference the file -->
```
