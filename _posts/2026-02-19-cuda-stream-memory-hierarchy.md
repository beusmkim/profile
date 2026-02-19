---
layout: default
title: "CUDA Streams and GPU Memory Hierarchy Awareness"
---

# CUDA Stream-Based Asynchronous Inference

## Problem
Blocking kernel execution degraded throughput in multi-request scenarios.

## Approach
- Implemented asynchronous CUDA streams
- Isolated preprocessing, inference, and postprocessing stages
- Reduced tensor copy operations
- Controlled memory reuse to avoid fragmentation

## GPU Memory Hierarchy Consideration
- Global memory latency impact
- Avoiding unnecessary memory transfers
- Understanding compute-bound vs memory-bound workloads

## Result
- Improved throughput stability
- Reduced latency variance under load
