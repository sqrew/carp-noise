# Examples

## Basic 2D Noise

Generating a simple 2D heightmap value:

```carp
(use Noise)

(let [state (make-noise 42)
      x 10.5
      y 20.1
      h (noise2d &state x y)]
  (IO.println &(format "Height at %f, %f is %f" x y h)))
```

## 3D Noise

Useful for volumetric noise or time-varying 2D noise:

```carp
(let [state (make-noise 99)
      time 1.23
      val (noise3d &state 0.5 0.5 time)]
  (IO.println &(str val)))
```

## Fractal Brownian Motion (FBM)

FBM combines multiple "octaves" of noise to create more natural-looking textures like clouds or terrain.

```carp
(let [state (make-noise 1)
      ;; 6 octaves, 0.5 persistence (diminishing returns), 2.0 lacunarity (increasing frequency)
      config (FBMConfig.init 6 0.5 2.0)
      val (fbm2d &state 0.01 0.01 &config)]
  (IO.println &(str val)))
```

## Seeding for Procedural Generation

You can create multiple independent noise states to ensure consistency across different biomes or layers:

```carp
(let [ground-noise (make-noise 100)
      cave-noise (make-noise 200)
      vegetation-noise (make-noise 300)]
  (do
    ;; Each use of these states is deterministic and independent
    ...))
```
