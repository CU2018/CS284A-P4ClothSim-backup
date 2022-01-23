# Project 4: Cloth Simulation
You can view the spec for this project at [Assignment 4: Cloth Simulation](https://cs184.eecs.berkeley.edu/sp21/docs/proj4).

![cover](/images/cover.gif)

In this project, a real-time simple cloth simulation is implemented with mass-spring system model. Starting from building the data structures to discretely represent the cloth, I then define and apply physical constraints (including `STRUCTURAL`, `SHEARING`, or `BENDING` ) on them, and apply numerical integration to simulate the way cloth moves over time. Meanwhile, collisions with other objects (plane and sphere) and self-collisions are also implemented.



# Part 1: Masses and Springs

In this part, the basic structure of cloth is built up with three types of constraints (including `STRUCTURAL`, `SHEARING`, or `BENDING`).

Here are the outputs of a horizontally flat cloth wireframe with different settings of enabled constraints.

| ![part1_1](/images/part1_1.png) | ![part1_2](/images/part1_2.png)  | ![part1_3](/images/part1_3.png) |
| :-----------------------------: | :------------------------------: | :-----------------------------: |
|      with all constraints       | without any shearing constraints | with only shearing constraints  |

An output of `scene\pinned2.json`

| ![part1_4](/images/part1_4.png) |
| :-----------------------------: |
|      `scene\pinned2.json`       |



# Part 2: Simulation via Numerical Integration

In this part, Verlet integration is implemented for integrating the physical equations of motion in order to apply the forces on our cloth's point masses. And then, figure out how they move from one time step to the next.

Here is a simulation process of the cloth with 4 ends pinned:

| ![part2_1](/images/part2_1.gif) |
| :-----------------------------: |
|      `scene\pinned4.json`       |

The appearance and behavior of the cloth can vary by modifying parameters, including the stiffness/resistance to deformation`ks` and `density`. While higher `ks` results in tight cloth that is less tend to stretch under gravity, higher `density` increases the downward gravitational force on the cloth and create more folds as shown below.

Varying `ks` with fixed `density` = 15

| ![part2_1](/images/part2_1.png) | ![part2_2](/images/part2_2.png) | ![part2_3](/images/part2_3.png) | ![part2_4](/images/part2_4.png) |
| :-----------------------------: | :-----------------------------: | :-----------------------------: | :-----------------------------: |
|           `ks` = 100            |           `ks` = 1000           |      `ks` = 5000 (default)      |          `ks` = 100000          |

Varying `density` with fixed `ks` = 5000

| ![part2_5](/images/part2_5.png) | ![part2_3](/images/part2_3.png) | ![part2_6](/images/part2_6.png) | ![part2_7](/images/part2_7.png) |
| :-----------------------------: | :-----------------------------: | :-----------------------------: | :-----------------------------: |
|          `density` = 5          |    `density` = 15 (default)     |         `density` = 30          |         `density` = 100         |



# Part 3: Handling Collisions with Other Objects

In this part, collisions with other objects (including plane and sphere) are implemented. At a high level, the `collide` method will determine whether or not a given point mass is inside the primitive. If it is, we adjust the point mass's position so that it stays just outside the primitive's surface, accounting for friction as we do so.

Colliding with sphere and plane (**without** self-collisions)

| ![part3_1](/images/part3_1.png) | ![part3_2](/images/part3_2.png) |
| :-----------------------------: | :-----------------------------: |
|       `scene\sphere.json`       |       `scene\plane.json`        |

Here is a simulation process of the cloth colliding with sphere (**without** self-collisions)

| ![part3_1](/images/part3_1.gif) |
| :-----------------------------: |
|       `scene\sphere.json`       |



# Part 4: Handling Self-collisions

In this part, self-collision of cloth is implemented with spatial hashing.

Here is a simulation process of the cloth placing vertically and colliding with the plane and itself. However, the jittering artifact is still noticeable. It could be improved with smaller step_of_time or better self-collision handling methods.

| ![part4_1](/images/part4_1.gif) |
| :-----------------------------: |
|   `scene\selfCollision.json`    |

With self-collision implemented, let's compare the sphere-cloth collision with and without self-collision. It's obvious that with collision, the part of cloth that is falling downward (below the sphere) is more natural and it's not colliding with itself any more.

| ![part3_1](/images/part3_1.gif) | ![part4_2](/images/part4_2.gif) |
| :-----------------------------: | :-----------------------------: |
|   **without** self-collision    |     **with** self-collision     |



# Part 5: Shaders

In this part, five different types of shaders are implemented using GLSL, including diffuse shading, Blinn-Phong shading, texture mapping, displacement and bump mapping, and environment-mapped reflections

| ![part5_1](/images/part5_1.png) |
| :-----------------------------: |
|         Diffuse Shading         |

| ![part5_2](/images/part5_2.png) |
| :-----------------------------: |
|       Blinn-Phong Shading       |

| ![part5_3](/images/part5_3.png) |
| :-----------------------------: |
|         Texture Mapping         |

| ![part5_411](/images/part5_411.png) |            ![part5_412](/images/part5_412.png)            |
| :---------------------------------: | :-------------------------------------------------------: |
|            Bump Mapping             |         Bump Mapping: does NOT change the vertex          |
| ![part5_421](/images/part5_421.png) |            ![part5_422](/images/part5_422.png)            |
|        Displacement Mapping         | Displacement Mapping: changes the vertex and the geometry |

|            ![part5_5](/images/part5_5.png)             |
| :----------------------------------------------------: |
| Environment-mapped Reflections (with cubemap textures) |

