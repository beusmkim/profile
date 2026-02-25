---
layout: project
title: "Satellite Data Center Siting — Distributed Geospatial Compute"
image: /assets/img/projects/dc-siting-placeholder.jpg
---

## Overview
A distributed processing pipeline for large geospatial datasets (ERA5) to score candidate locations for data center siting. The focus was memory-safe processing and scalable execution rather than a single optimization algorithm.

## Problem
ERA5 datasets (zarr) are large and not suitable for naive in-memory processing:
- Single-machine runs were slow and memory-heavy
- Loading broad geographic ranges increased memory footprint
- Iteration speed was limited by I/O and aggregation bottlenecks

## Diagnosis
The bottleneck was dominated by **data volume and memory behavior**:
- Geospatial aggregation created large intermediate arrays
- Broad bounding boxes inflated I/O and compute cost
- Lack of partitioning led to uneven workloads and memory spikes

## Approach
### Tile-based partitioning
- Split data into tiles to bound memory usage per task
- Enabled incremental aggregation and caching

### Distributed execution (AWS Batch + S3)
- Executed tiles in parallel with job-based orchestration
- Stored intermediate outputs in S3 for reproducibility and reprocessing

### Scoring abstraction
- Designed node-level scoring so features can be added without reworking the pipeline
- Kept pipeline modular for future accelerator-backed workloads

## Result
- Scalable execution model: parallelizable tasks with bounded memory per tile
- Improved iteration speed via modular recomputation and S3-backed intermediates
- A foundation suitable for extending into larger regions or additional features

## Key insight
For large-scale geospatial workloads, performance is often a function of partitioning and dataflow design. Correctly bounding memory per task and decoupling compute from storage creates stable scalability without requiring complex optimization algorithms.
