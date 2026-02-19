---
layout: project
title: "Satellite Data Distributed Pipeline for Data Center Siting"
summary: "Distributed preprocessing pipeline using AWS Batch and S3 for scalable geospatial/time-series workload execution."
period: "2026"
role: "Infra/Data Pipeline"
stack: "AWS Batch, S3, Python, Zarr/Xarray"
image: /assets/img/projects/Tamna-eye_mainpage.png
links:
  - label: "Repository"
    url: "https://github.com/username/REPO"
order: 80
featured: true
---

## Hardware Efficiency Focus

This project focused on scalable execution of large satellite and weather datasets used for scoring candidate data center sites.
The engineering target was reliable throughput under increasing data volume through partitioned distributed processing.

## Emphasis Bullets

- Built a distributed preprocessing flow on AWS Batch + S3 to execute large data transformations as parallelizable job units.
- Structured ROI cut, resampling, and aggregation stages for scale-out execution and reproducible outputs.
- Separated source, intermediate, and final artifacts to reduce pipeline coupling and improve execution reliability.
- Converted heavy raw inputs into node-level features ready for downstream scoring and validation steps.
- Designed the pipeline for sustained data throughput as workload size grows, instead of single-machine processing limits.

## Quantified Impact

- This project did not claim a single latency or VRAM percentage metric.
- The measurable outcome was scale-out readiness and stable distributed execution behavior for large preprocessing workloads.

## Silicon-Validation Alignment

Large-scale validation workflows depend on reliable data preparation pipelines.
This project supports that need by establishing distributed, repeatable preprocessing that can feed hardware-aware model evaluation at scale.
