# Reconfigurable Mixed-Precision 2×2 Weight-Stationary Systolic MAC Array

**Tiny Tapeout submission | SkyWater 130nm | TTSKY26c shuttle**

## Project Documentation

- [Read the full project documentation](docs/info.md)
- [Verification summary and report](docs/verification.md)

## What is this?

This project implements a **2×2 weight-stationary systolic array** of multiply-accumulate (MAC) processing elements that can switch between two numeric precisions at runtime.

Each processing element holds a stationary weight and streams activations through the array, accumulating partial sums as data flows from PE to PE. This is the classic **systolic dataflow** used in modern NPU/TPU-style accelerators, scaled down to fit within a single Tiny Tapeout tile.

### Key Features

- **2×2 systolic MAC array**
- **Weight-stationary dataflow**
- **Runtime-reconfigurable mixed precision**
- Supports **4-bit and 2-bit operation**
- **Shared masked multiplier** for both precision modes
- **Zero-operand skip mechanism** to reduce unnecessary switching activity
- Designed within a single Tiny Tapeout tile

Rather than instantiating separate multipliers for 4-bit and 2-bit operation, precision switching is implemented through a **shared masked multiplier**. The same multiplier hardware is reused for both modes, with input masking gating the unused bits when operating at lower precision.

A **zero-operand skip mechanism** gates the accumulate path whenever an operand is zero, avoiding unnecessary switching activity during those cycles.

## Research Contribution

2×2 systolic arrays have appeared previously on Tiny Tapeout. This project combines:

1. Runtime-reconfigurable mixed precision
2. Shared masked multiplier hardware
3. Weight-stationary dataflow
4. Zero-operand skip gating

The combination is designed to provide multiple precision modes and reduce unnecessary switching activity while remaining within a fixed Tiny Tapeout silicon budget.

A feature-comparison table against prior systolic-array submissions is included in the project documentation.

## Design Summary

| Parameter | Details |
|---|---|
| **Top Module** | `tt_um_dilip951_cpu_systolic_array` |
| **Array Size** | 2×2 |
| **Precision Modes** | 4-bit and 2-bit |
| **Dataflow** | Weight-stationary |
| **Standard Cells** | 608 |
| **Flip-Flops** | 62 |
| **Die Area** | ~117 × 128 µm |
| **PDK** | SkyWater `sky130A` |
| **Shuttle** | TTSKY26c |
| **Verification** | Cocotb |
| **Functional Tests** | 2/2 passing |

## Physical Design and Verification

The design was verified through the Tiny Tapeout GitHub Actions flow using **LibreLane 3.0.5**.

The following checks were completed successfully:

- DRC
- LVS
- Antenna checks
- GDS generation
- Tiny Tapeout precheck (**15/15**)
- Gate-level simulation (`gl_test`)
- Design viewer

The results were independently cross-checked using an **OpenLane2 Colab flow**, with matching flip-flop count and die area, and a clean LVS result.

## What is Tiny Tapeout?

Tiny Tapeout is an educational project that aims to make it easier and cheaper than ever to get digital and analog designs manufactured on a real chip.

To learn more and get started, visit:

https://tinytapeout.com

## Resources

- [Tiny Tapeout FAQ](https://tinytapeout.com/faq/)
- [Digital Design Lessons](https://tinytapeout.com/digital_design/)
- [Learn How Semiconductors Work](https://tinytapeout.com/siliwiz/)
- [Tiny Tapeout Community](https://tinytapeout.com/discord)
- [Build Your Design Locally](https://www.tinytapeout.com/guides/local-hardening/)
