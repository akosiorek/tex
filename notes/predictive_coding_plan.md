# Predictive Coding plan

The goal of the project is to design a probabilistic predictive coding framework and examine its properties both empirically and analytically. To do so, we require several components:
  * Tasks and datasets to perform any examination; they should allow both quantitive and qualitative evaluation.
  * Fitness metrics to track the properties we wish to improve.
  * Baseline to compare against; We're interested in beating them in any type of metrics.

## Tasks
A number of tasks and corresponding datasets to perform the examination. Tasks should be organised to test different properties of predictive systems:
  * Extrapolating motion
  * Handling occlusion
  * Respecting other objects and boundaries, e.g. bouncing
  * Inferring any external forces
  * Capturing correlations between moving objects

## Datasets
Datasets should be simple, preferably similar for every task, such that there is not too big a burden on visual processing itself. Images should be small and time-series not too long, to allow rapid iteration.
  * Flying balls of different colours
  * Closed/open boundaries of the box
  * Possible physical or only visual obstacles
  * External forces e.g. gravity
  * Internal forces e.g. electric potentials, where balls attract or repel each other

## Baselines    
We need good baselines; otherwise the experiment doesn't make much sense. We are not advocating using probabilistic inference per-se, so we don't necessarily require deterministic baselines to compare to.

What we want to do is:

  * Show that a temporal baseline exhibits internal covariate shift of temporal signals
  * Show that a multi-layer baseline exhibits internal covariate shift between different layers

If we are able to show the above, we can start experimenting with predictive-coding approach, which has the potential of alleviating these issues.

We should also include a baseline with an additional cost on predicting state, as predictive-state models have been recently shown to achieve better performance.

## Predictive Coding
Once we establish that there are some issues with temporal models or at least establish what the baseline level of performance is, we can start looking into predictive-coding models. There are many possible architectures leading to different dependencies between latent and observed variables as well as different possible interactions between dependent variables. We need to explore some varieties, compare results and reason about the origin of differences in performance.

## Summary
I think it is interesting from a statistical perspective, because it tries to improve performance of a huge class of model by incorporating (a small bit of) structure into the problem.
