# PHOTEX

**Photonic Inference — Volumetric Optical Neural Networks**

PHOTEX develops photonic inference accelerators using 3D volumetric holographic interference. Our Holo-Pod architecture achieves orders-of-magnitude improvements in speed, energy, and parameter density versus conventional GPUs.

---

## Overview

| Metric | NVIDIA H100 | PHOTEX Holo-Pod (1 cm³) |
|--------|-------------|-------------------------|
| **Parameters** | ~20–35B | **90 T** (45 T with 50% error correction) |
| **Latency** | ~7–10 ms | **1.3 ns** |
| **Energy** | ~mJ/pass | ~pJ–fJ (99% reduction) |
| **Throughput** | 100–150 TPS | 7.5 M – 375 M TPS |

---

## What We're Building

- **PHOTEX* — A compact photonic inference accelerator using volumetric holographic crystals
- **Angular Spectrum Method (ASM)** — Wave propagation at the speed of light
- **Volumetric multiplexing** — 3D stacked crystals with angular multiplexing for trillion-parameter capacity
- **Error correction** — 50% density for redundancy; multi-run averaging for 99% accuracy

---

## Documentation

| Document | Description |
|----------|-------------|
| [Wave Propagation & ASM](docs/01_Wave_Propagation_and_ASM.md) | Mathematical foundations: Helmholtz equation, propagation transfer function, evanescent waves |
| [Benchmark Results](docs/02_Benchmark_Results.md) | Simulation results vs NVIDIA H100: memory, energy, speed, error correction |

---

## Technology Highlights

1. **Wave optics** — Light propagation via Angular Spectrum Method (O(N log N) per step)
2. **Phase masks** — Trainable diffractive layers; physical realization via SLMs, DOEs, metasurfaces
3. **Interference as attention** — I = \|E₁ + E₂\|² naturally encodes dot-product attention
4. **1 cm³ cube** — 90 trillion parameters (1,000 layers × 900 angular channels × 100M params/layer)

---

## References

- Goodman, J. W. (2005). *Introduction to Fourier Optics*
- Lin, X., et al. (2018). "All-optical machine learning using diffractive deep neural networks." *Science*
- Miller, D. A. B. (2017). "Attojoule optoelectronics"

---

## License

See [LICENSE](LICENSE).
