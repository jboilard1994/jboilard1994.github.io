---
title: Machine Vision – Industrial Quality Control
description: Computer vision applications for industrial quality control.
---

I worked on a machine vision system for detecting missing welds on steel joists in an industrial production line.

## My Role
End-to-end ownership of the vision pipeline, from data preparation and model development to evaluation under extreme class imbalance and on-premise deployment.

## Mockup Demo
Due to confidentiality constraints, this is a sanitized mockup representative of the real system and challenges.

![System Demo](/media/machine_vision/generic_exemple.gif)

## Constraints
- Weld presence/absence detection in harsh industrial conditions  
- Variable lighting and environmental noise  
- High-speed production line  
- Extreme class imbalance (<1% missing welds)  
- Near-zero tolerance for false negatives  
- Mandatory on-premise deployment

## Tech Stack
PyTorch, Python, Pandas, Docker, Kubernetes, Vertex AI

## Results
While exact metrics cannot be disclosed, the system **outperformed manual inspection** and met reliability requirements for production use.

## On-Premise Architecture
Inference runs on-premise to ensure reliability and avoid network-related disruptions.

![On-Premise Deployment](/media/machine_vision/on-premise.png)

1) **Model serving (AI inference)** : Reusable across all solutions that share the same model design (e.g. different use cases using the same architecture but different weights).

2) **Prediction post-processing** : Raw predictions often need to be aggregated into a single decision (e.g. multiple predictions for the same object that may disagree). The technical structure is reusable across use cases, while business rules vary.

3) **Camera orchestration** : Provides a standardized camera abstraction, compatible with use cases involving single or multiple cameras. Fully reusable across use cases. Can also be deployed independently (with its database) for preliminary image collection initiatives.

4) **Main control application** : Responsible for handling all remaining business logic and application-specific needs of the use case.

## Cloud Deployment Pipeline
Cloud infrastructure used for staging, but also data storage, model training, and MLOps workflows.

![Cloud Pipeline](/media/machine_vision/cloud_pipeline.png)
