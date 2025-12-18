---
title: Machine Vision
description: Computer vision applications for object detection and analysis.
---

# Computer Vision – Industrial Quality Control

I previously worked on a machine vision system designed to detect the presence or absence of welds on steel joists in an industrial production environment.

## My Role
I was responsible for the end-to-end design and implementation of the machine vision pipeline, including data preparation, model development, evaluation under class imbalance, and deployment to on-premise infrastructure.

## Mockup Demo
Due to industrial secrecy constraints, the demonstration below is a legally sanitized mockup of a generic machine vision system.  It closely reflects the type of solution and challenges involved in the real-world project I worked on.

![System Demo](/media/machine_vision/generic_exemple.gif)

## Constraints
- Detect weld presence/absence on steel joists under real production conditions with significant environmental disturbances
- High variability in lighting conditions
- High-speed production line
- Highly imbalanced data distribution (probability of missing welds < 1%)
- Very low tolerance for false negatives (missed welds), with performance required to exceed manual inspection
- On-premise deployment required due to network reliability constraints

## Tech Stack
Vertex AI, Docker, Kubernetes, PyTorch, Python, Pandas

## Results
While exact performance metrics cannot be disclosed for legal reasons, the deployed system **surpassed manual quality control in detecting missing welds**, meeting the reliability requirements necessary to replace human inspection.

## Deployment Architecture
The inference system is deployed **on-premise** to ensure reliability and avoid disruptions caused by unstable internet connectivity, allowing data to be processed directly at the edge.

![On-Premise Deployment](/media/machine_vision/on_premise.jpeg)

For long-term data storage, model training, and MLOps workflows, a cloud-based pipeline is used.

![Cloud Pipeline](/media/machine_vision/cloud_pipeline.png)
