# The Baseline Fluctuation Mystery

## The empirical observation

UV absorbance elution data shows a subtle baseline fluctuation that is a **scaled derivative** of the elution curve:

$$\text{baseline fluctuation}(t) \propto \frac{dc}{dt}$$

This has been confirmed empirically across multiple SEC-SAXS datasets but has never been explained theoretically.

Notably, the fluctuation scale can be **both positive and negative** — the signal is bipolar, exactly as a derivative of a peak would be (positive on the rising edge, negative on the falling edge, or vice versa).

## Working hypothesis: temperature variation via non-isothermal LKM

The non-isothermal Lumped Kinetic Model (LKM) predicts that elution causes **temperature variation** in the column. This temperature variation is a candidate mechanism — possibly among others — for the observed baseline fluctuation.

The reasoning (still to be verified):

1. **Non-isothermal LKM predicts temperature variation.** The energy balance in the LKM contains a source term driven by adsorption/desorption kinetics. As solute elutes, the rate of adsorption $\partial q / \partial t$ releases or absorbs heat, producing a temperature fluctuation that should be derivative-shaped with respect to the concentration profile.
2. **Temperature variation may affect UV detection.** If the temperature fluctuation propagates to the detector cell, it could alter refractive index or absorbance characteristics, producing the observed baseline artifact.

The gap between step 1 and step 2 is significant: the LKM predicts temperature variation *in the column*, but the column and the UV detector are connected by a tube of some length. How does the temperature signal propagate through the tube to the detector, and how does it affect the measurement at the UV radiation spot?

## Rejected alternative: UV radiation as heat source

Before pursuing the column-to-detector propagation hypothesis, a simpler alternative was tested:

> **Could the UV radiation itself cause the temperature variation at the detector spot?**

The `heat-simulation/` notebooks simulate heat diffusion from a localised source (modelling UV radiation at the detector). The result: **the temperature pattern does not look derivative-shaped**. This rejects the hypothesis that UV-induced heating at the detector spot is the cause of the observed dc/dt-proportional baseline fluctuation.

This negative result is important because it narrows the search: the fluctuation is not generated locally at the detector.

## The column temperature hypothesis — and its flaw

The remaining candidate is that the derivative-shaped temperature variation originates **in the column** (as predicted by the non-isothermal LKM) and propagates through the connecting tube to the detector.

However, an expert objection challenges this: **the temperature variation should be reduced to a negligible level during solution transfer through the connecting tube**. Thermal equilibration with the tube walls would smooth out the small temperature signal long before it reaches the detector.

This leaves the mystery in a puzzling state:
- The non-isothermal LKM is the **only known mechanism** that produces a derivative-shaped temperature signal.
- But the physical path from column to detector (through the tube) appears to **destroy that signal** before it can be observed.
- No alternative explanation for the dc/dt-proportional baseline fluctuation has been identified.

## What is established vs. what is hypothesised

| Claim | Status |
|-------|--------|
| Baseline fluctuation ∝ dc/dt | **Empirically confirmed** |
| Non-isothermal LKM predicts temperature variation in the column | **Established** (Ahmad et al. 2019 and others) |
| Temperature variation is derivative-shaped w.r.t. concentration | **Likely** (follows from the energy balance source term) |
| UV absorbance depends on temperature | **Established** (Li et al. 2012: ~7% change over 18°C range) |
| UV radiation at detector causes the fluctuation | **Rejected** (heat simulation shows non-derivative shape) |
| Column temperature variation propagates to detector via tube | **Doubtful** (expert: temperature dissipates in the tube) |
| This temperature variation causes the observed UV baseline fluctuation | **Hypothesis — weakened by tube dissipation objection** |
| The detailed mechanism at the detector (refractive index? direct absorbance?) | **Unknown** |

## Connection to the broader research programme

If confirmed, this would connect to **Paper (b)** (Realistic Physical Constraints) in the [paper strategy](../modeling-vs-model_free/PAPER_VISION_DISCUSSION.md):
- The LKM framework would explain not just peak shape but also subtle baseline effects.
- It would demonstrate that physics-based modelling reveals phenomena invisible to isothermal models.

## Repository structure

```
baseline-fluctuation-mystery/
├── README.md              ← this file (problem statement and hypothesis)
├── reference_papers/      ← collected papers on thermal effects and UV-temperature sensitivity
└── heat-simulation/       ← tests the "UV radiation as heat source" hypothesis (rejected)
    ├── heat-1.ipynb       ← 1D heat equation, explicit method (tutorial baseline)
    ├── heat-2.ipynb       ← heat + concentration coupling, temperature at detector
    └── heat-3.ipynb       ← 3D visualization of concentration-temperature coupling
```

## References

**Non-isothermal LKM — temperature variation in columns:**

Ahmad, A. G., Qamar, S., & Seidel-Morgenstern, A. (2019). "Linearized non-equilibrium and non-isothermal two-dimensional model of liquid chromatography for studying thermal effects in cylindrical columns." *J. Liquid Chromatography & Related Technologies*, 42(13–14), 436–451.

Qamar, S., Kiran, N., Anwar, T., Bibi, S., & Seidel-Morgenstern, A. (2018). "Theoretical investigation of thermal effects in an adiabatic chromatographic column using a lumped kinetic model incorporating heat transfer resistances." *Industrial & Engineering Chemistry Research*, 57(6), 2287–2297.

**UV absorbance temperature dependence:**

Li, X.-X., Wang, Y., Xu, P.-P., Zhang, Q.-Z., Nie, K., Hu, X., Kong, B., Li, L., & Chen, J. (2012). "Effects of temperature and wavelength choice on in-situ dissolution test of Cimetidine tablets." *J. Pharmaceutical Analysis*, 3(1), 71–74.

**Other (relevance to be clarified):**

Rossi, B., et al. (2024). "Operando UV Resonance Raman study of DNA-ionic liquids gels." *J. Molecular Liquids*, 398, 124209.

## Status

- ✅ Empirical observation confirmed (baseline ∝ dc/dt)
- ✅ Non-isothermal LKM identified as candidate explanation for temperature variation in column
- ❌ UV radiation at detector as heat source — rejected (heat-simulation result is not derivative-shaped)
- ⚠️ Column-to-detector propagation — expert says temperature dissipates in the connecting tube
- 🔑 No alternative explanation for the derivative shape has been identified
- 🔲 Gap: mechanism by which temperature affects UV measurement at the detector spot (Li 2012 provides partial answer: ε_a depends on refractive index which depends on temperature)
- 🔲 Quantitative comparison with real SEC-SAXS data
- 🔲 Clarify relevance of Rossi 2024
