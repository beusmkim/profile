---
layout: project
title: "High-Strain-Rate Material Characterization — Experimental Calibration & Model Validation"
image: /assets/img/projects/shpb.png
permalink: /projects/11-shpb
category: hardware
priority: 2
---

## Overview

This project focused on characterizing high-strain-rate material behavior using Split Hopkinson Pressure Bar (SHPB) experiments and calibrating a constitutive model under dynamic loading conditions.

The objective was to translate experimental measurements into a predictive simulation model capable of representing strain-rate dependent behavior.

---

## Problem

Material behavior under high strain rates differs significantly from quasi-static conditions.

Key challenges:

- Experimental stress–strain curves exhibited rate dependency
- Existing model parameters failed to accurately predict dynamic behavior
- Finite element simulations deviated from experimental results

A calibration and validation workflow was required.

---

## Experimental Setup

- Split Hopkinson Pressure Bar (SHPB) apparatus
- High strain-rate impact testing
- Stress–strain curve acquisition under dynamic loading
- Signal processing to extract wave propagation data

---

## Diagnosis

Analysis revealed:

- Significant strain-rate sensitivity in material response
- Nonlinear hardening behavior under impact conditions
- Existing SK constitutive parameters insufficient for high-rate modeling

The discrepancy between experimental and simulation results indicated parameter misalignment.

---

## Approach

### Constitutive Model Calibration

- Applied SK material model
- Fitted strain-rate dependent parameters to experimental data
- Iteratively adjusted coefficients to minimize error between experiment and simulation

### Finite Element Validation

- Implemented calibrated model in Abaqus
- Simulated impact conditions replicating SHPB setup
- Compared simulated stress–strain curves with measured results

---

## Result

- Reduced simulation error against experimental stress–strain curves
- Improved predictive accuracy under dynamic loading
- Established validated parameter set for high strain-rate conditions

---

## Limitations

- Validation constrained to tested strain-rate range
- Model assumptions limited to isotropic behavior
- Further microstructural modeling required for extreme conditions

---

## Key Insight

Accurate system behavior under extreme conditions requires empirical measurement, parameter calibration, and iterative validation.

The workflow—measure → model → calibrate → validate—mirrors hardware performance validation processes, where empirical data informs model correction.
