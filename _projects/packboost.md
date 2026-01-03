---
title: Custom Gradient Boosting
description: A domain-specific gradient boosting algorithm for constraints beyond standard libraries.
---

# Custom Gradient Boosting with PackBoost

PackBoost is a domain-specific gradient boosting algorithm designed to handle constraints not supported by standard libraries.

<div style="text-align: center;">
  <div style="border: 2px solid #ddd; border-radius: 8px; padding: 10px; display: inline-block; overflow: hidden;">
    <img src="/media/PackBoost/boosting_trees.gif" alt="Gradient Boosting Trees" style="display: block; margin: -10px; max-width: calc(100% + 20px);">
  </div>
  <div>
    <small style="opacity: 0.7;">
      Gradient boosting decision trees and aggregation of weak learners.
    </small>
  </div>
</div>

<hr style="margin: 3rem 0;">

## Design Choices

PackBoost was developed for a public data science competition focused on financial markets. Its design reflects this context:

1. **Synchronized ensemble feature sampling**
   - Ensemble of weak learners for robustness  
   - Feature synchronization to encourage orthogonality
2. **Era-aware split selection**
   - Improved robustness across market regimes
3. **Round-forward sample paths**
   - Enables massive parallelization  
   - Preserves orthogonality across boosting rounds

<hr style="margin: 3rem 0;">

## Ensemble Feature Synchronization

For a given round, features are never reused across folds. When  
`split_feature_candidates << total_features`, this enforces approximate orthogonality between ensemble members.

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

<hr style="margin: 3rem 0;">

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

<hr style="margin: 3rem 0;">

## Shared Tree Paths for Parallel Training

Instead of recursive tree growth, PackBoost reuses tree paths from previous rounds. This non-optimal strategy enables large-scale parallelization.

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

<hr style="margin: 3rem 0;">
