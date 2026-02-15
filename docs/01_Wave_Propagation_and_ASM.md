# Wave Propagation and Angular Spectrum Method (ASM)

## 1. Wave Optics Fundamentals

### 1.1 The Wave Equation

Light propagation is governed by the wave equation:

```
∇²E - (1/c²)∂²E/∂t² = 0
```

For monochromatic waves (single frequency), this simplifies to the **Helmholtz equation**:

```
(∇² + k²)E = 0
```

where `k = 2π/λ` is the wavenumber.

### 1.2 Complex Representation

Monochromatic waves are represented as complex exponentials:

```
E(x, y, z, t) = A(x, y, z) × exp(j(ωt - k·r))
```

For computational purposes, we work with the complex amplitude:

```
u(x, y, z) = A(x, y, z) × exp(-jφ(x, y, z))
```

where:
- **A(x, y, z)**: Amplitude (real, positive)
- **φ(x, y, z)**: Phase (real, in radians)

### 1.3 Intensity

The intensity (power per unit area) is proportional to the squared amplitude:

```
I(x, y, z) = |u(x, y, z)|² = A²(x, y, z)
```

---

## 2. Angular Spectrum Method (ASM)

### 2.1 Mathematical Derivation

The ASM solves the Helmholtz equation in the frequency domain. Starting from the wave equation in free space:

```
∂²u/∂z² = -(∂²u/∂x² + ∂²u/∂y² + k²u)
```

Taking the 2D Fourier transform in the (x, y) plane:

```
U(fx, fy, z) = ∫∫ u(x, y, z) exp(-j2π(fx·x + fy·y)) dx dy
```

The wave equation becomes:

```
∂²U/∂z² = -[(2πfx)² + (2πfy)² - k²]U
```

This has the solution:

```
U(fx, fy, z) = U(fx, fy, 0) × H(fx, fy, z)
```

where the **propagation transfer function** is:

```
H(fx, fy, z) = exp(j × kz × z)
```

and:

```
kz = sqrt(k² - (2πfx)² - (2πfy)²)
```

### 2.2 Evanescent Waves

When `(2πfx)² + (2πfy)² > k²`, we have:

```
kz = j × sqrt((2πfx)² + (2πfy)² - k²)
```

These are **evanescent waves** that decay exponentially with distance. They do not propagate and are filtered out in the ASM implementation.

### 2.3 Algorithm

1. **Input**: Complex field `u(x, y, 0)` at plane z = 0  
2. **FFT**: Compute angular spectrum `U(fx, fy, 0) = FFT[u(x, y, 0)]`  
3. **Multiply**: Apply transfer function `U(fx, fy, z) = U(fx, fy, 0) × H(fx, fy, z)`  
4. **IFFT**: Transform back `u(x, y, z) = IFFT[U(fx, fy, z)]`  

**Complexity**: O(N log N) per propagation step, where N is the number of pixels.

### 2.4 Implementation Parameters

| Parameter | Value |
|-----------|-------|
| Wavelength | 405 nm |
| Pixel size | 1 µm |
| Refractive index | 1.5 |

---

## 3. Phase Modulation (Diffractive Layers)

A diffractive layer introduces a position-dependent phase shift:

```
u_out(x, y) = u_in(x, y) × exp(j × φ(x, y))
```

where φ(x, y) is the phase mask. Phase masks can be realized using Spatial Light Modulators (SLMs), Diffractive Optical Elements (DOEs), or metasurfaces.

---

## 4. Optical Attention via Interference

When two waves superpose, the intensity includes an interference term:

```
I = |E1 + E2|² = |E1|² + |E2|² + 2×Re(E1×E2*)
```

The cross-term `2×Re(E1×E2*)` encodes interference. For complex vectors Q and K, `Re(Q · K*)` matches this term—similar vectors produce constructive interference (high attention). Wave interference thus implements dot-product attention without explicit matrix multiplication.
