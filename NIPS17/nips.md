# Tuesday 5/12

## Optimisation Track 10:40 am

### Matrix Est from Linear Measurements

m - num entries, n^2 matrix dim

underdetermined problem with m < n^2
need additional constraints, e.g. fill missing entries with zeros to get a unique solution

* GD on X gives 0 train error, high test error, GD - gradient descent
* GD on f(U), factorisation of X, gives also 0 train error but low test error => better generalisation
* GD on f(U) converges to minimum nuclear norm solution (wtf?)

### Linear Convergence of Frank-Wolfe algorithms...
no idea what that is about...

### Acceleration and.. on Stochastic Dynamics?
- continuous time model for stochastic Optimisation-study
 interaction between noise and acceleration rates

 1) Mirror Descent:
 * dynamics is a coupling between two variables
 * z accumulates gradient
 * mirror map is a mapping from the dual space to the constraint set; it's identity in the euclidean space

2) Accelerated Mirror Descent:
 * take same dynamics and replace primal variable by weighted average of mirror trajectory so far
 * learning rate in the dual space and averaging rate params

3) inject noise to get stochastic dynamics
* get stochastic differential equation
* accelerated dynamics are not robust to noise; Nesterov dynamics with noise diverge
*

### When Cyclic Coord Descent outperforms Randomised Coord descent
* CD - optimise iteratively, in one dim at a time
* deterministic order: cyclic CD
* random order of dims: randomised CD

* convergence rates suggest that CCD is O(n^2) slower than RCD
* but empirically, CCD is often better than RCD. why, or at least, when?


## Algo and Opt Track 14:50

### Submodular Nets #155
* define a set function on image segments as the total activation on those segments minus some reference activation
* subset selection is NP hard and func evals are expensive (DNN inference)
* => streaming optimisation
* STREAK - streaming thresholding algorithm with arbitrarily good approximation guarantee
* greedy submodular minimises a discrete derivative

### Unified Appproach to Interpreting Model Predictions #34
* Interpretability is important for a lot of vendors
* Models are either accurate or interpretable, but not both
* We can toggle (mask) inputs to learn how features affect outputs; we can also set weights to different features to quantify their influence, and then we can use the sum instead of the actual outputs
* We can apply the above to features; applicate to Additive Feature Attribution Methods (it's a class of models that uses sums of features)
* Feature weights can be seen as Shapely values from game theory
* SHAP -> unification of many different approaches to model Interpretability
* SHAP evaluates prediction after toggling all inputs, one at a time, and correcting for N! possible combinations, but it doesn't actually evalaute all N!
* Shapely values are expensive to compute, MC sampling of Shapely has high variane, LIME is biased; SHAP is approximate, unbiased and much faster to compute then Shapely.
* github/slundberg/shap


### Differentiable Learning of Submodular models #157
* Goal; incorporate discrete opt into NNs
* Submodular minimisation is a layer that does discrete optimisation on its inputs and outputs discrete outputs, a vector of ones and zeros
* convex relaxation to have outputs in [0, 1], so that the thresholded output is the same as discrete would be; that allows to compute the gradients for the backward pass

## Theory Track

### Clustering Billions of sth from DNA for Storage? #74
* clustering for edit distance, different than Hamming distance
* edit distance is hard, performance is O(n^2) which is too bad for large datasets
* nearly linear time, scales well, streamaing?
* binary embedding -> cheaper hamming distance as an approximator to edit distance


### On the complexity of learning NNs
* Guarantees for training NNs by SGD when learning data generatred by small NNs? Weird...


### Multiplicative Weight Updates...
no idea what it is about; 2-player game and Nash equilibria, but MWU... ?

### Mutual Info Estimation in mixtures
* estimates the MI derivative from samples, hmm

## Deep Learning and Algo track, 16:20

### VGG James Talk
* really cool, will follow up

### Eigen... Alexander... #125
* How can we quantify the visibility of image distortions?
* Instead of taking MSE between target and input image, it;s better to find an embedding and take the norm of the embedding diff
* Train neural nets to predict human sensitivity to visual distortions
* models: biological nets, VGG but not refitted but with weighted MSE, generic NN
* compare the above; rigorous method for comparision
* generic CNN does best on a test set, but the goal here it to generalize to different datasets
* Fisher information can be used to map sensitivity of the model into the pixel space; if we take a levelset in a feature space and map it via Fisher into pixel space, it gives us info about relative sensitivity to different pixel changes;
* we can take biggest and highest eigenvectors and compare sensitivity to human subjects; if high ev is aligned with high threshold in humans and low with low threshold, the model is well aligned -> rigorous metrics for comparision
* important is the difference between detection thresholds between the model and humans
* biological On-Off gated model is the best aligned with humans, awesome!!!!!!!!!!!!!!!!!!!

### Interp and Globally Optimal Pred... by Raymond... #82
* what's the goal? -> unified framework for texture grounding
* text for image desription and images
* find bounding boxes of objects referred to by the description?
* find weight associating each word of the description with image concepts, or features
* this leads to an energy function per pixel; a bounding box should correspond to a location with low cumulative energy
* find bounding boxes by an efficient sub-window search algo
* word-concept weights are interpretable
* loss used is a structured SVM-like loss

## SPOTLIGHTS

### Towards accurate binary convolutional neural networks #101
* not here due to visa issues

### DL for Precipitation Nowcasting #110
* nowcast - 0-6h forecast
* MovingMNIST++, moving with rotation and illumination changes <- is it a standardised dataset? find out!


### Poincare Embeddings for Learning Hierarch Reprs #104
* graph embeddings and such
* goal: simult capture similarity and hierarchy in the embedding space from unsupervised data
* hyperbolic space: a continuous version of trees, can capture hierarchy unlike euclidean sapce
* poincare distance - rescaled euclidean distance, based on where the points are in a ball; points that are close to the boundary tend to be far apart from each other, points that are inside are closer: variable relative size of neighberhoods, which gives the hierarchy, nice -> leavs have small neighbourhoods

### Deep Hyperspherical Learning
* simple mod of NNs, speeds up convergence and shortens training time
* motivated by fourier transforms -> phase contains the most discriminative info, as opposed to the magnitude
* neural net that work only on the angles between kernel parameters and local patch
* it's not a new idea...

### What Uncertainties Do we Need in Bayesian Deep Learning #95
* Yarin Gal, nice self-PR

### One-Sided Unsupervised Domain Mapping
* unsupervised image to image translation
* idea: if we take a pair of images and apply style transfer, the distance between the images between the mapping should be the same as the one after the Mapping
* it allows to use a one-sided mapping which is different from both-sided cycle-gans
* cycle-gans are not appropriate, because if we map a zebra to a horse and lose stripes, it will be impossible to map it back, but a one-sided mapping doesn't have this property
* Loss: general GAN loss + distance preservation term

### Deep Mean-Shift priors for image restoration #86
* nice
































# Notes
* do aux stuff during brakes; focus on the proceedings whenever you can
