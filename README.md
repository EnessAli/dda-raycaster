# DDA Raycaster

A Wolfenstein-3D style 3D rendering engine implemented in C using the **Digital Differential Analyzer (DDA)** ray casting algorithm and the MiniLibX graphics library.

## Algorithm

The engine casts one ray per screen column using the DDA algorithm for efficient grid traversal:

1. **Ray direction** is calculated from the camera plane and player angle
2. **DDA step** determines distance to next cell boundary (delta distances)
3. **Wall hit detection** finds the exact grid cell and side (NS/EW) hit
4. **Projection** calculates wall slice height using perpendicular distance to avoid fisheye effect
5. **Texture mapping** samples the correct pixel column from a loaded XPM texture

```
perpWallDist = (mapX - posX + (1 - stepX) / 2) / rayDirX
lineHeight   = (int)(screenHeight / perpWallDist)
```

## Features

- Four directional wall textures (North, South, East, West)
- Configurable floor/ceiling colors via scene file
- Smooth 60FPS rendering with delta-time movement
- Mouse look (horizontal rotation)
- Configurable map via `.cub` scene definition file
- Clean scene parser with descriptive error messages

## Scene File Format (`.cub`)

```
NO ./textures/north.xpm
SO ./textures/south.xpm
WE ./textures/west.xpm
EA ./textures/east.xpm

F 220,100,0
C 225,30,0

111111
100001
1N0001
111111
```

## Controls

| Key | Action |
|-----|--------|
| `W/A/S/D` | Move forward/left/back/right |
| `←/→` | Rotate camera |
| `ESC` | Exit |

## Build & Run

```bash
make
./cub3D maps/example.cub
```

## Tech Stack

`C` `MiniLibX` `DDA Algorithm` `Ray Casting` `XPM Textures` `Math`

