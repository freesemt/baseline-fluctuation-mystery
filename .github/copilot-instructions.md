<!-- AI Context Standard v0.8 - Adopted: 2026-03-25 -->
# AI Assistant Initialization Guide

**Purpose**: Initialize AI context for the baseline-fluctuation-mystery repository  
**Created**: February 24, 2026

---

## What this repository is about

An unsolved mystery in SEC-SAXS: the UV absorbance baseline shows a fluctuation proportional to dc/dt (the time-derivative of the concentration profile). The fluctuation is bipolar (both positive and negative). No theoretical explanation has been confirmed.

## Key documents

1. **[README.md](README.md)** — Full problem statement, hypotheses tested, current status, and references. **Read this first.**

## Current hypothesis status

- **Non-isothermal LKM** (Ahmad 2019, Qamar 2018) predicts derivative-shaped temperature variation in the chromatographic column — this is the only known mechanism producing the right shape
- **UV absorbance depends on temperature** (Li 2012) — confirms the detector would respond to temperature changes
- **BUT**: an expert objection says the temperature signal dissipates in the connecting tube between column and detector
- **UV radiation at detector** as local heat source — **rejected** by heat simulations in `heat-simulation/`

## Repository structure

```
baseline-fluctuation-mystery/
├── .github/
│   └── copilot-instructions.md  ← this file (auto-loaded by GitHub Copilot)
├── README.md              ← problem statement and hypothesis tracking
├── reference_papers/      ← collected PDFs (non-isothermal LKM, UV-temperature)
└── heat-simulation/       ← tests the "UV radiation as heat source" hypothesis (rejected)
    ├── heat-1.ipynb       ← 1D heat equation, explicit method
    ├── heat-2.ipynb       ← heat + concentration coupling
    └── heat-3.ipynb       ← 3D visualization
```

## Relationship to other repos

This repo is part of the **molass workspace** (8 repos). The baseline fluctuation mystery is referenced in [PAPER_VISION_DISCUSSION.md](../modeling-vs-model_free/PAPER_VISION_DISCUSSION.md) §8 as potential supporting evidence for Paper (b) (Realistic Physical Constraints).
