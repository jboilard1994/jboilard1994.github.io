---
title: Custom Gradient Boosting
description: A domain-specific gradient boosting algorithm designed to address constraints not handled by standard libraries.
---

# Custom gradient boosting with PackBoost

Packboost is a domain-specific gradient boosting algorithm designed to address constraints not handled by standard libraries.

<div style="text-align: center;">

<div style="border: 2px solid #ddd; border-radius: 8px; padding: 10px; display: inline-block; overflow: hidden;">

<img src="/media/PackBoost/boosting_trees.gif" alt="System Demo" style="display: block; margin: -10px; max-width: calc(100% + 20px);">

</div>

<div>
<small style="opacity: 0.7;">*Visualization of a gradient boosting decision tree for a regression problem, showing how the model partitions the feature space and makes predictions, and how the outputs of multiple weak learners are aggregated together.*</small>
</div>

</div>

<hr style="margin: 3rem 0;">

## Design philosophy

The public Data science competition I participate in is related to investing in stock markets. It was designed with these characteristics in mind :

1. PackBoost incorporates an ensemble where feature sampling is synchronized. We hypothesize that this increases the orthogonality of the ensemble of weak-learners, which accomodate the high noise-to-signal ratio of the dataset.
2. The data is time-stratified, where an interaction can be highly useful in an era but not in others. To avoid learning such interactions, Packboost incorporates era-aware split selection methods. 
3. To be competitive, models need to be highly optimized. Part of this optimization involves hyperparameter selection and feature selection. However, the dataset is quite large (Nearly 100 million rows, >2000 feature columns). PackBoost contains a novel training method allowing to train a tree atr all depths simultaneously using pseudo-optimial splits based on the previous round's splits.

<hr style="margin: 3rem 0;">

### Ensemble feature synchronization

The key of this design element is that there is no repetition of features between fold. We believe that when `split_feature_candidates << total_features`, this method loosely imposes orthogonlity between models of the ensemble

<div style="text-align: center;">

<div style="border: 2px solid #ddd; border-radius: 8px; padding: 10px; display: inline-block; overflow: hidden;">

<img src="/media/PackBoost/fold_synchronization.png" alt="System Demo" style="display: block; margin: -10px; max-width: calc(100% + 20px);">

</div>

<div>
<small style="opacity: 0.7;">Pre-sampled feature schedule for each fold and each depth</small>
</div>

</div>

<hr style="margin: 3rem 0;">

### Era-aware splitting criterion

We use a splitting criterion based on [insert reference] for determining the best split at each node, which significantly alters which splits are optimal.

<div style="text-align: center;">

<div style="border: 2px solid #ddd; border-radius: 8px; padding: 10px; display: inline-block; overflow: hidden;">

<img src="/media/PackBoost/era_splitting.png" alt="System Demo" style="display: block; margin: -10px; max-width: calc(100% + 20px);">

</div>

<div>
<small style="opacity: 0.7;">Example of splitting data at a given node. Using traditional splitting criterions, a single split is evaluated using a single global score. Using an era-aware implementation, a score for each era is obtained, leading to different splits depending on how the scores are aggregated</small>
</div>

</div>

<hr style="margin: 3rem 0;">

### Sharing of tree paths allowing massive parallization  

Traditional tree growth methods evaluates splits recursively at each depth level. We use a non-optimal method which recycles previous round's tree paths for each sample. 

<div style="text-align: center;">

<div style="border: 2px solid #ddd; border-radius: 8px; padding: 10px; display: inline-block; overflow: hidden;">

<img src="/media/PackBoost/train_iterations.png" alt="System Demo" style="display: block; margin: -10px; max-width: calc(100% + 20px);">

</div>

<div>
<small style="opacity: 0.7;">Example of splitting data at a given node. Using traditional splitting criterions, a single split is evaluated using a single global score. Using an era-aware implementation, a score for each era is obtained, leading to different splits depending on how the scores are aggregated</small>
</div>

</div>

<hr style="margin: 3rem 0;">

### Results

Coming soon