# Approximate Inference Workshop

## Netflix: VAEs for Movie Recommendation
* VAEs work better than Gaussian Matrix Factorisation; they are mostly better than denoising autoencoders, too
* denoising autoencoders are a little bit better when there is a lot of user activity, e.g. a lot of data -> in that case, the prior is a bit constraining and hurts the performance; the less user activity (Data), the better the VAE with respect to DAE

## Poster Spotlights

### AdaGeo: adaptive geometric learning for optimisation and sampling
* Sampling is hindered in high-dim spaces; but the should lie a manifold -> use a GPLVM to recover the manifold
* use the GPLVM info to recover the manifold

### Variational Inference for DPGMMs with Coresets
* goal: scale up VI via coresets
* coresets capture both large and small components, the latter would be normally missed by the approx posterior
* approx ELBO can be reduced to approx ELBO for a specific GMM

### Generic finite approx for practical BNPs
* we can handle infinities in BNP by some finite approximation based on the data, e.g. truncated finite approx or non-nested finite approx
* truncated approx are quite easy for a wide variety of bnp priors, but non-nested are more convenient; no general recipies for constructing them
* show how to construct non-nested finite approx and show how to implement in STAN

### Efficient acquisition rules for model-based approximate Bayesian computation
* goal: bayesian inf for a simulation model with an intractable likelihood; simulation is comput costly so we can't use MC
* formulate the ABC problem in Bayesian framework
* surrogate modelling to account the ocomputational uncerttainty in the abc posterior
* new eval locations ar eselected to minimise the expected uncerttainty
* practical algo under GP modelling assumptions

### Boosting VI: an opt perspective
* boosting: use a mixture of approx distributions instead of just one, so that we can leverage boosting and trade approximation with accuracy and get a very expressive family of models
*

### Exploration and exploitating in adaptive importane sampling
* draw samples, adapt the proposal according to previous samples
* taget pi i learnt throght a sequence of queries at x_t
* there's a tradeoff explortation exploitation
* Partition a sample space into K disjoint spaces; the proposal is a mixture onto the subspaces
* use RL, reward: importance weights, arm for a banding: a subspace; boost probability of a subspace based on the upper confidence bound

### ...GMC for multimodal posterior Sampling
* HMC has problems with multimodal distributions; we need to use continuous tempering
* to leverage dataset, we need Nose-Hoover thermostat, but it results in biased samples
* systematic integration for accurate samplling: fokker-plank equation -> we can sample accuratly for the posterior

### VI with Stein mixtures
* Stein VAEs used particle-filter approximation; this extends the algo to be able to modify parameters of the variational posterior and thereby come up with a stein mixture approximation

### Binary Bouncy Particle Sampler
* particle moves along a bound and occasinally bounces, where the bounce events come from a poisson distribution with rate dependent on the gradient of the probability
* non-reversible; no detailed balance
* velocity is +/-1; there's no bounce when the velocity points into lower energy regions, but it has positive bouncing prob when going to higher energy regions
* contribution: generalise the bouncy continuous particle to binary

### Inference Trees: Adaptive Inference with Explortation
* MCTS to improve SMC; improve long-range dependencies we can deal with and improving beyond what you can get by adapting the proposal
* split the target space and run sampling in different regions
* combined this with stratified sampling
* explicitly allocate resources to each of the target regions
* explore uncertain regions instead of just using best estimates so far in a greedy way
* in an online fashion, learn hierarchical partition space by constrcting a partition tree

### Structured VAEs for Beta-Bernoulli Process - IBP!!!!!!!!!!!!!!!!!!!!!!!!!!!
* stick-breaking representation to generate features and associated feature vectors
* gumbel-softmax for discrete... I should use that, too
* github.com/rachtsingh/ibp_vae

### Natural Gradients via Variational Predictive Distribution

## Taylor Residual Estimators via Automatic Differentiation
* truncated Taylor expansion is not perfect, introduces errors (residuals dependent on the higher order terms)
* the bulk of variance of the estimator sits in those residuals; residuals are of course intractable, but we can MC approx them
* Assuming we can compute f and its first order taylor expansion, we can estimate its residual

## Antti Honkela: Differential privacy and Bayesian learning
* sensitivity - given two datasets different only by a single sample, what is the maximum differnece in the function value?
* add noise to the function value scaled by the sensitivity removes any detectable difference, thereby making dataset differences unidentifiable
* bayesian approach: differentially-private bayesian approximation, constructed such that log of the ratio of probabilities for two perurbed dataset is smaller than eps

## Yixin Wang: Frequentist Consistency of Variational Bayes
* VB does not enjoy many theoretical guarantees; here we show consistency and asymptotic... in the limit of infinite data
* experiments on topic models often assume infinite numer of documents
* MCMC is theoretically guaranteed, but on some experiments on topic models VB converges faster than MCMC => guarantees *should* exist for VB.... yeah, right :)
* WHY is VB posterior consistent????
* as more data comes in, the exact posterior converges to a point mass (in the infinite data regime), that is it has no variance
* point masses are factoriazable => exact posterior sits in our approximating familiy in the inf data limit
* with infinity data, the variational family does contain the truth, somehow surprisingly, and VB is consistent, e.g. converges to the true estimate; AWESOME :D
* three conditions: one is that the prior on parameters puts nonzero (or enough) mass on the region around the true population estimate; the true posterior has also be asymptotic to normal and has to be consistently testable; that is the true and non-true estimates have to be distinguishible with inf data


## Panel Discussion
