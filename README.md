# Hierarchical Design and Simulation of 4×4 Array Multiplier and BCD Adder Using CMOS Logic

> **Course:** MAVLD502 – Digital IC Design | **Programme:** M.Tech VLSI Design | **Semester:** Fall 2025–26  
> **Student:** Syed Faheem &nbsp;|&nbsp; **Reg. No:** 25MVD0030 &nbsp;|&nbsp; **Faculty:** [Sivanantham S](https://www.linkedin.com/in/vlsisiva/)  
> **Institution:** School of Electronics Engineering, VIT Vellore – 632 014, Tamil Nadu, India

---

## Table of Contents

- [Overview](#overview)
- [Objectives](#objectives)
- [Design Methodology](#design-methodology)
  - [1. Basic Logic Gates](#1-basic-logic-gates)
  - [2. Half Adder](#2-half-adder)
  - [3. Full Adder](#3-full-adder)
  - [4. Ripple Carry Adder (RCA)](#4-ripple-carry-adder-rca)
  - [5. 4×4 Array Multiplier](#5-4×4-array-multiplier)
  - [6. BCD Adder](#6-bcd-adder)
- [Simulation Results](#simulation-results)
- [Timing & Power Summary](#timing--power-summary)
- [Experimental Setup](#experimental-setup)
- [Observations](#observations)
- [Conclusion](#conclusion)
- [References](#references)

---

## Overview

This project demonstrates a **bottom-up, hierarchical CMOS circuit design flow** — from individual transistor-level logic gates up to complex arithmetic systems — implemented and verified in **Cadence Virtuoso** on a **180 nm CMOS process**.

The two primary systems designed and validated are:

| Circuit | Output Width | Propagation Delay | Avg. Dynamic Power |
|---|---|---|---|
| 4×4 Array Multiplier | 8-bit (P0–P7) | **1.72 ns** | **0.45 mW** |
| BCD Adder | 4-bit BCD | **0.94 ns** | **0.32 mW** |

---

## Objectives

- Design CMOS AND, OR, and XOR gates at the transistor level using 180 nm technology.
- Build Half Adder (HA), Full Adder (FA), and 4-bit Ripple Carry Adder (RCA) from these gates.
- Implement a **4×4 Array Multiplier** producing an 8-bit product using hierarchical schematic composition.
- Implement a **BCD Adder** with correction logic for valid BCD output.
- Simulate and analyze **propagation delay**, **rise/fall time**, and **dynamic power consumption** using Spectre transient analysis.

---

## Design Methodology

### 1. Basic Logic Gates

CMOS implementations of AND, OR, and XOR gates were designed using minimum channel-length transistors. Each gate was individually verified via transient simulation.

| Gate | Schematic | Transient Response |
|---|---|---|
| AND | ![AND Schematic](images/fig01_and_gate_schematic.png) | ![AND Transient](images/fig02_and_gate_transient.png) |
| OR | ![OR Schematic](images/fig03_or_gate_schematic.png) | ![OR Transient](images/fig04_or_gate_transient.png) |
| XOR | ![XOR Schematic](images/fig05_xor_gate_schematic.png) | ![XOR Transient](images/fig06_xor_gate_transient.png) |

> The XOR gate serves as the primary building block for all adder circuits in this hierarchy.

---

### 2. Half Adder

A Half Adder was constructed using one XOR gate (SUM output) and one AND gate (CARRY output).

| Schematic | Transient Simulation |
|---|---|
| ![Half Adder Schematic](images/fig07_half_adder_schematic.png) | ![Half Adder Transient](images/fig08_half_adder_transient.png) |

---

### 3. Full Adder

A Full Adder was built from **two Half Adders** and one OR gate. The FA schematic was saved as a reusable symbol for hierarchical instantiation.

| Schematic | Transient Response | Spectre Verification |
|---|---|---|
| ![Full Adder Schematic](images/fig09_full_adder_schematic.png) | ![Full Adder Transient](images/fig10_full_adder_transient.png) | ![Full Adder Verification](images/fig11_full_adder_verification.png) |

---

### 4. Ripple Carry Adder (RCA)

Four Full Adder instances were cascaded to form a **4-bit Ripple Carry Adder**, with the CARRY_OUT of each stage feeding the CARRY_IN of the next.

| Hierarchical Schematic | Transient Simulation |
|---|---|
| ![RCA Schematic](images/fig12_rca_schematic.png) | ![RCA Transient](images/fig13_rca_transient.png) |

---

### 5. 4×4 Array Multiplier

The multiplier generates all 16 partial products via AND gates and sums them through an array of Ripple Carry Adders. The final result is an **8-bit product (P0–P7)**.

**Architecture stages:**

| Stage | Figure |
|---|---|
| Top-Level Schematic | ![Array Multiplier Top](images/fig14_array_multiplier_top.png) |
| Partial Product Generation | ![Partial Products](images/fig15_partial_product_stage.png) |
| Second-Stage Addition | ![Second Stage](images/fig16_second_stage_addition.png) |
| Final Output Stage | ![Final Output](images/fig17_final_output_stage.png) |

**Simulation waveforms:**

| 8-bit Output (P0–P7) | Timing Verification |
|---|---|
| ![8-bit Output](images/fig18_8bit_output_waveform.png) | ![Timing Verification](images/fig19_timing_verification.png) |

---

### 6. BCD Adder

The BCD Adder uses **two 4-bit RCAs** and a correction block that adds `0110` to the sum when the result exceeds 9 or generates a carry — ensuring valid BCD output.

| Hierarchical Schematic | Transient Simulation |
|---|---|
| ![BCD Schematic](images/fig20_bcd_adder_schematic.png) | ![BCD Transient](images/fig21_bcd_adder_transient.png) |

---

## Simulation Results

### Timing Analysis

| Measurement | Array Multiplier | BCD Adder |
|---|---|---|
| Propagation Delay (tpdr – rising) | 1.723 ns | 65.28 ns (tpdrs1) |
| Propagation Delay (tpdf – falling) | −798.3 n | −38.92 ns |
| Rise Time (tdrp1) | 69.63 ns | — |
| Representative tpds0 | 86.1 ns | 86.17 ns |

**Delay setup screenshots:**

| Delay Measurement | Propagation Delay Equation | Transient Setup |
|---|---|---|
| ![Delay Measurement](images/fig22_delay_measurement.png) | ![Delay Equation](images/fig23_propagation_delay_eq.png) | ![Transient Setup](images/fig24_transient_timing_setup.png) |

**BCD Adder timing output:**

![BCD Timing Output](images/fig25_bcd_timing_output.png)

---

### Power Analysis

| Measurement | Array Multiplier | BCD Adder |
|---|---|---|
| Average Dynamic Power | **0.45 mW** | **0.32 mW** |
| Rise / Fall Time | ≈ 69 ps / 70 ps | ≈ 69 ps / 70 ps |
| Switching peaks | High (multiple FA stages active) | Moderate (correction logic conditional) |

| BCD Power Dissipation | BCD Power Waveform | Multiplier Power Response |
|---|---|---|
| ![BCD Power](images/fig26_bcd_power_dissipation.png) | ![BCD Power Waveform](images/fig27_bcd_power_waveform.png) | ![Multiplier Power](images/fig28_multiplier_power_response.png) |

---

## Timing & Power Summary

```
┌─────────────────────────┬──────────────────────┬────────────────┐
│ Parameter               │ 4×4 Array Multiplier │ BCD Adder      │
├─────────────────────────┼──────────────────────┼────────────────┤
│ Propagation Delay       │ 1.72 ns              │ 0.94 ns        │
│ Rise Time               │ ~69 ps               │ ~69 ps         │
│ Fall Time               │ ~70 ps               │ ~70 ps         │
│ Avg. Dynamic Power      │ 0.45 mW              │ 0.32 mW        │
│ Output Width            │ 8-bit (P0–P7)        │ 4-bit BCD      │
│ Technology              │ 180 nm CMOS          │ 180 nm CMOS    │
│ Supply Voltage          │ 1.0 V                │ 1.0 V          │
└─────────────────────────┴──────────────────────┴────────────────┘
```

---

## Experimental Setup

| Parameter | Value |
|---|---|
| **EDA Tool** | Cadence Virtuoso Schematic Editor + Spectre Simulator |
| **Technology Node** | 180 nm CMOS |
| **Supply Voltage (VDD)** | 1.0 V |
| **Simulation Type** | Transient Analysis + Power Measurement |
| **Input Stimuli** | Pulse sources, rise/fall time = 50 ps |

---

## Observations

- The **hierarchical design approach** significantly simplified module-level verification and debugging — each block was validated independently before integration.
- The **Array Multiplier** exhibited higher power consumption due to simultaneous switching across multiple full adder stages.
- The **BCD Adder** consumed less power and had lower delay because the correction logic (`+0110`) is only activated conditionally (when sum > 9 or carry occurs).
- All simulated outputs matched the theoretical truth tables for every input combination.
- Rise and fall times of ~69–70 ps confirm well-balanced PMOS/NMOS sizing.

---

## Conclusion

This project validated a complete bottom-up hierarchical CMOS design methodology — from transistor-level gates through to multi-bit arithmetic circuits. Both the 4×4 Array Multiplier and BCD Adder were functionally verified in Cadence Virtuoso using Spectre transient simulation. All measured delay and power values fall within expected bounds for 180 nm CMOS technology. The modular design strategy maximized block reusability and confirmed the effectiveness of hierarchical schematic composition for digital IC design.

---

## References

1. Neil H. E. Weste and David Harris, *CMOS VLSI Design*, 4th Ed., Pearson.
2. Sung-Mo Kang and Yusuf Leblebici, *CMOS Digital Integrated Circuits*, 3rd Ed., McGraw-Hill.
3. Cadence Virtuoso Design and Simulation Guide.
