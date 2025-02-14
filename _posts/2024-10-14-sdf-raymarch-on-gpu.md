---
title: Raymarching 3D Texture SDF on fragment shader 
author: andreas
date: 2024-10-14 17:00:00 +0900
categories: [Guide, Mesh Distance Field]
tags: [graphics, sdf, raymarch, shadow, guide, mesh distance field, signed distance field, opengl, c++]
---
While working on the generation of 3d texture SDF on fragment shader, I decided to finish the raymarch SDF on gpu first. I just finished it, so it should still contain some bugs. Will look into it later-ish


The object I'm using is just some random object I made in 30 seconds in blender. The 3d texture SDF is still generated on the CPU side for now, hence I can't go too high since it takes forever to generate an SDF texture

| original object | ![Original object](../assets/img/post_img/2024-10-14-sdf-raymarch-on-gpu/original-model.png) |
| 64 steps 16x16x16: | ![16x16x16](../assets/img/post_img/2024-10-14-sdf-raymarch-on-gpu/16.png) | 
| 64 steps 32x32x32: | ![32x32x32](../assets/img/post_img/2024-10-14-sdf-raymarch-on-gpu/32.png) |
| 64 steps 64x64x64: | ![64x64x64](../assets/img/post_img/2024-10-14-sdf-raymarch-on-gpu/64.png) |

Some observation:
- The higher the texture resolution, the higher the lag. Something is definitly wrong in the code somewhere since the SDF raymarch algorithm shouldn't be affected by the texture size since it's just a texture sample. Will probably look into this. I suspect higher resolution = higher step count (instead of terminating early).  
- Certain artifacts still appearing regardless of the texture resolution. Probably implies there's a bug in the code somewhere.

---
