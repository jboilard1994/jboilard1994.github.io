---
title: Custom Gradient Boosting with PackBoost
description: A domain-specific gradient boosting algorithm for constraints beyond standard libraries.
---


PackBoost is a domain-specific gradient boosting algorithm designed to handle constraints not supported by standard libraries.

<div style="text-align: center;">
  <div style="border: 2px solid #ddd; border-radius: 8px; padding: 10px; display: inline-block; overflow: hidden;">
    <img src="/media/PackBoost/boosting_trees.gif" alt="Gradient Boosting Trees" style="display: block; margin: -10px; max-width: calc(100% + 20px);">
  </div>
  <div>
    <small style="opacity: 0.7;">
      In PackBoost, one gradient boosting round is an aggregation of multiple decision trees.
    </small>
  </div>
</div>

## Design Choices

PackBoost was developed for a public data science competition focused on financial markets. Its design reflects the following context :

1. **Synchronized ensemble feature sampling**
   - Ensemble of weak learners for robustness  
   - Feature synchronization to encourage orthogonality of boosting rounds
2. **Era-aware split selection**
   - Improved robustness across market regimes
3. **Round-forward sample paths**
   - Enables massive parallelization  
   - Mitigates overfitting by validating prior splits against new feature subsets

## Ensemble Feature Synchronization

For a given round, features are never reused across folds. When  
`split_feature_candidates << total_features`, this enforces approximate orthogonality of the step taken by the ensemble at every boosting round.

<div style="text-align: center;">
  <div style="border: 2px solid #ddd; border-radius: 8px; padding: 10px; display: inline-block; overflow: hidden;">
    <img src="/media/PackBoost/fold_synchronization.png" alt="Feature Synchronization" style="display: block; margin: -10px; max-width: calc(100% + 20px);">
  </div>
  <div>
    <small style="opacity: 0.7;">
      Pre-sampled feature schedule per fold and tree depth.
    </small>
  </div>
</div>

## Era-Aware Splitting Criterion

Splits are selected using an era-aware criterion ([reference TBD]). Instead of a single global score, splits are evaluated per era and then aggregated.

<div style="text-align: center;">
  <div style="border: 2px solid #ddd; border-radius: 8px; padding: 10px; display: inline-block; overflow: hidden;">
    <img src="/media/PackBoost/era_splitting.png" alt="Era-Aware Splitting" style="display: block; margin: -10px; max-width: calc(100% + 20px);">
  </div>
  <div>
    <small style="opacity: 0.7;">
      Era-level scoring leads to different optimal splits than global criteria.
    </small>
  </div>
</div>

## Shared Tree Paths for Parallel Training

Instead of recursively growing trees, PackBoost reuses decision paths from previous rounds. While intentionally non-optimal, this strategy enables massive parallelization and mitigates overfitting by validating prior splits against new feature subsets.

<div style="text-align: center;">
  <div style="border: 2px solid #ddd; border-radius: 8px; padding: 10px; display: inline-block; overflow: hidden;">
    <img src="/media/PackBoost/train_iterations.png" alt="Parallel Tree Training" style="display: block; margin: -10px; max-width: calc(100% + 20px);">
  </div>
  <div>
    <small style="opacity: 0.7;">
      Reusing paths across rounds enables parallel split evaluation.
    </small>
  </div>
</div>


