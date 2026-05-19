# carp-noise

A fast, seeded Simplex Noise implementation for the [Carp](https://github.com/carp-lang/Carp) programming language.

## Features

- **Seeded Noise State**: Independent noise generators that do not rely on global RNG state.
- **2D & 3D Simplex Noise**: Implementation based on the canonical Simplex algorithms.
- **Fractal Brownian Motion (FBM)**: Composable fractal noise with configurable octaves, persistence, and lacunarity.
- **Performance**: Uses unsafe array access for hot paths and avoids allocations during sampling.

## Installation

Clone this repository into your project or add it as a submodule:

```bash
git submodule add https://github.com/sqrew/carp-noise.git
```

## Usage

```carp
(load "carp-noise/noise.carp")
(use Noise)

(defn main []
  (let [state (make-noise 12345)
        val (noise2d &state 0.5 0.5)]
    (IO.println &(Double.to-string val))))
```

### Fractal Noise (FBM)

```carp
(let [state (make-noise 123)
      config (FBMConfig.init 6 0.5 2.0)
      val (fbm2d &state 0.1 0.2 &config)]
  (IO.println &(Double.to-string val)))
```

## Testing

Run the test suite with:

```bash
carp -x test/noise_test.carp
```

## License

This project is licensed under the MIT License.
