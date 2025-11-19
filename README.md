# Superhero Flight System - Unreal Engine 5

I developed a camera-relative flight system enabling intuitive superhero-style aerial movement in UE5.

## Overview

This project implements a fully-functional flight system that prioritizes **intuitive player control** through camera-relative input. The character naturally follows camera orientation for vertical movement, eliminating the need for separate keys like Q/E for up/down control.

[Recording 2025-11-19 194425](https://github.com/user-attachments/assets/67972ec7-0f63-42c8-8ce2-ce0e83186540)

## Key Features!


- **Camera-Relative Flight**: Character movement follows camera pitch and yaw for natural 3D navigation
- **Seamless Locomotion Blending**: Smooth transitions between ground walking and aerial flight
- **Animation-Driven System**: Eight-directional blend space animations with speed-based variation
- **Native Character Movement Component**: Built entirely using UE5's Character Movement system without custom C++ code
- **Responsive Controls**: Precise acceleration/deceleration with configurable max flight speed

## Technical Architecture

### Why This Approach Works

Most flight implementations suffer from **decoupled input handling** where camera direction doesn't align with movement direction. This system solves that by:

1. **Decomposing camera rotation** into separate horizontal (yaw) and vertical (pitch) components
2. **Reconstructing movement vectors** in world space based on these calculated angles
3. **Using conditional input routing** via Select nodes to apply flying-specific movement calculations while maintaining ground locomotion logic

The result: your character naturally flies toward where you're looking, with vertical camera tilt directly controlling altitude.

### Core Systems

**Flight Activation** (Character Blueprint - Event Graph)
- Double-tap jump to toggle flight mode
- Sets Character Movement to "Flying" mode
- Configures rotation settings for aerial perspective

**Movement Input** (Character Blueprint - Input Handling)
- Gets controller rotation (yaw + pitch)
- Calculates forward/right vectors relative to camera
- Applies vectors to Character Movement with 1500 UU/s max speed

**Animation System** (Animation Blueprint)
- Reads movement direction and current velocity
- 8-direction blend space with idle and fast animations
- Automatically blends between walking and flying states

## Configurable Parameters

| Parameter | Default | Purpose |
|-----------|---------|---------|
| Max Fly Speed | 1500 UU/s | Maximum flight velocity |
| Flying Acceleration | 3000 UU/s² | Braking deceleration when slowing down |
| Double-Jump Counter | 3 | Number of jumps before flight triggers |

## How to Set Up

1. **Character Movement Settings**: Enable "Can Fly" and set max fly speed to 1500
2. **Input Mapping**: Bind spacebar to Jump action
3. **Animation Blueprint**: Create blend space with provided animations mapped to direction/speed axes
4. **State Machine**: Implement conditional blend between ground and flying locomotion

## Technical Advantages

- **No custom C++ code required** - entirely Blueprint-based for easy modification
- **Optimal performance** - uses native engine systems rather than custom movement calculations
- **Scalable** - easily add features like flight stamina, boost mechanics, or hover states
- **Animation-friendly** - respects character rotation and blend space interpolation

## Screenshots

<img width="1700" height="732" alt="image" src="https://github.com/user-attachments/assets/40a824f1-039c-49cd-bf92-310f59c6c36a" />

- Updated "Move" function accomadating new Z-axis

<img width="1891" height="764" alt="image" src="https://github.com/user-attachments/assets/c816dbf7-6f25-428d-8560-160f9f10b698" />

- Updated "Event Graph", Blueprint switches flight mode with camera-relative controls.

<img width="1380" height="869" alt="image" src="https://github.com/user-attachments/assets/67d02526-a406-4f40-a0d7-e7f09c91f74b" />

- Flying Animation Blend Space




