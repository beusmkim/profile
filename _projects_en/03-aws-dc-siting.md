---
layout: project
title: "Satellite Data Center Siting — Partitioned Large-Scale Compute Design"
image: /assets/img/projects/dc-siting-placeholder.jpg
category: hardware
priority: 4
---

## Overview

A distributed geospatial computation pipeline for evaluating data center site suitability using ERA5 satellite datasets.

The focus was scalable partitioned execution and memory-safe processing under large dataset constraints.

---

## Problem

ERA5 datasets (zarr format) are large and not suitable for naive in-memory processing.

Observed issues:

- High memory footprint during wide-region aggregation
- Slow iteration cycles due to monolithic processing
- Memory spikes during intermediate tensor creation

---

## Diagnosis

Performance was dominated by data movement and intermediate aggregation size.

The bottleneck was not computational complexity, but partitioning strategy and dataflow design.

---

## Approach

### Tile-Based Partitioning

- Divided geospatial data into bounded tiles
- Constrained per-task memory usage
- Enabled incremental aggregation

### Distributed Execution

- Used AWS Batch for parallel task execution
- Stored intermediate artifacts in S3
- Designed recomputation boundaries for modular iteration

### Abstraction Layer

- Built node-level scoring abstraction
- Enabled future feature expansion without architectural changes

---

## Result

- Horizontally scalable processing pipeline
- Bounded memory per task
- Improved iteration speed via modular recomputation

---

## Insight

For large-scale workloads, partitioning and dataflow architecture define scalability ceilings more than raw compute.

Bounding memory per execution unit creates predictable performance behavior.
