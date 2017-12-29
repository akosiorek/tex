# Bayesian Deep Learning Workshop

## IWAE is not always the best by Tom Rainforth
* theoretically, IWAE bound improves training of the generative model but not the recognition model as the number of samples K increases
* it corresponds to the distribution of gradients for the recognition netowork; the probability of the gradient for the recognition network pointing in the right direction decreases as the number of particle increases
* intuitively, it can be explained by the fact that the higher number of particles K marginalises out the recognition model; i.e. in the infinite limit of number of samples the recognition model doesn't matter

## Horshoe weight priors <---------- LOOK AT IT FOR AIR!!!!!!!!!
* mixture of Gaussians with different scales
* encourages the weights to converge to zero values
* results in lower KL-div value for weights that go to zero simply because there is higher probability mass on zero weights in the prior
* for VAE with this prior for MNIST, the reconstruction for the least active units is just black, whereas for the N(0, 1) prior the reconstruction corresponds to the mean-digit; this is something I could directly use in my AIR project as prior for the what latents

* they also showed that the predictive uncertainty for bigger models is bigger just because there are more parameters to be uncertain about; the horseshoe prior fixes this issue
* number of active units is still proportional to the model size e.g. 7 for 10k units, 70 for 100k units

## Uncertaintity quantification by Max Welling
* Kingma, Salimans, Welling 2015: Variational Dropout and the local reparam trick <- lookup
* we can prune a neural model by imposing an inverse prior of weights, where the prob of a parameter is inversly proportional to its magnitude; compression rate reaches 280x
* Deep Compression paper: a bayesian insprised approach that doesn't actually give a posterior distribution; it gives up to 700x compression rates without affecting accuracy
* Bayes is a very good tool to both have uncertainty estimates and compress neural nets; but there are no benchmarks to test that
* it's unclear why neural net compression is possible at all

## Poster Spotlight Talk
### Improved Bayesian Compression
* Compression by optimising th eELBO when choosing relevant prior
* Soft-weight sharing: Gaussian-mixture prior on delta weight posterior <--- very similar to attention on model params?
### Noisy Natural Grad via VI
* weight updates of bayesian neral nets can be derived as noisy versions of gradient-based optimisers like ADAM or K-FAC
### Approx Grad for raining Implicit Models


## Entropy-SG(L)D Optimizes the Prior of a (Valid) PAC-Bayes Bound - read the paper !!!!!!!!!!!!!!!!!!!!!!!!
* sgd pefrorms some kind of approx inference and find an approximation Q to the true posterior P
* generalisation error fro Q bounded approx by 1/m KL[Q||P]
* given data S we can find a provably good clasifier Q by optimising the PAC-Bayes bound wrt Q
* choose P to be a prior scale mixture of Gaussians centerd at w0 and Q to be a gaussian
* minimise empirical risk plus KL penalty and an extra term (from P being mixture approximated by a union bound)
* when we optimise, we can evaluate the final emipirical risk and compute confidence bounds; they are loose but non-vacuous
* IDEA: Bayes theory (including PAC-Bayes) often assumes that a prior is a true prior, i.e. it's chosen without seeing the data (it's independent of the data distribution). That means that if we use e.g. type-2 ML or if we choose our prior based on the data distribution, whatever bounds we have becomes invalid. However, we can use differentially-private data-dependent priors to validate the prior distribution. That does not seem to be an issue in VAEs but might still be worth exploring or at least understanding: read the paper
* related to variational dropout

## Recent Advances in Autoregressive Generative Models
* Discretized logistic mixture Salimants et al 2017 <- look


## Deep Kernel Learning by Russ Salakhutdinov
* combine the inductive biases of deep archtectures with nonparametric flexibility of GPs
* gp prior + likelihood(as a function of the function given by the prior) => gp posterior
* likelihood gives importance weights for functions returned by the prior, thereby giving a posterior distribution over functions
* learning: sample functions from the prior and optmise the log marginal likelihood wrt kernel parameters
* log of marginal likelihodo -> inverse of a NxN matrix -> O(N^3) -> cannot scale beyond couple k points
* randomised methods, low-rank approx, structure preserving, variational approx for scaling it up
* we can use the structure andto solve linear systems and compute log-determinans, e.g. Kronecker structure or Toeplitz
* e.g. Toeplitz cov matrix is structured and we can levrage that for efficiency
* if inputs x lie on a D-dimensional grid, then the gram matrix K decomposes into a kronecker product of D matrices of lower dim
* exploit the structure through SVD to compute determinant and efficiently solve a linear system
* Alternatively, you can also introduce m inducing points and approx K(X, X) as K(X, U) K(U, U)^{-1} K(U, X), where inversion is now O(m^3), with m << N

deep kernels
* transform into x through a function g implemented as a neural net; use this feature repr as an input of the kernel
Scalable learning: use an m x m deep gram matrix and interpolate that into a higher-dim space by doing K = M K_U M^T, where M is an interpolation matrix with only 4 nnz elements per row
* we can solve the inverse of K in O(1), iteratively with  << n iterations via conjugate gradients
* we can use a relatively many inducing points and still have more or less fixed-time inference

* you can just train a DNN and feed the output into a kernel, but training through the kernel tends to further improve performance, and quite a lot

* tends to be a bit better than DNN without GPs... in every case??
* can also stick a GP on a DBN

## Panel Discussion
* YW: MCMC has a bad rep; it's solving a harder problem because it's trying to sample from the full posterior, while VI approx are fitted to only a single mode; it might be possible to do sth similar with MCMC; it's not good to be dogmatic Bayesian
* YLC: energy-based models are much more flexible and we can regularise them by having priors on the energy landscape, but we don't have to worry about normalisation until the very end
* YW: people use improper priors and don't really worry about normalisations
* ZG: they're all equivalent ways of thinking; Bayesians really care about averaging rather than choosing; delay decision-making as much as we can; in the bayeian sense, procrastination is the optimal policy :)
* Bayesian approach is the separation between decision making and model choosing; it's optimal only if the model is correct, which never really happens
* model for both VAE and GAN is a *nonlinear hierarchical factor analysis model*, but people tend to mix the model with the algorithm, and it's the algorithm that is different for VAE and GAN; both assume different ways to try to get around the normalising constant: energy for GANs, factorisation for VAEs
* generator in a GAN is a very smart way of sampling very high-dim distribution; YW: it's not very smart, it's just importance sampling with iid samples
* 

* Lecun is very defensive; to the point that he makes mistakes in what he's saying; both Zoubin and YW wer ereally disturbed but and disagreed by what he said about VAEs and GANs; he doesn't like sampling, nor normalising constants


# Disentangled Representations Workshop
## Doina Precup on Temporal Abstractions
* sinlge-step prediction leads to error accumulation and large errors/bad actions when unrolling
* multi-step rollouts and backprop of error from that leads to better temporal abstractions
* option models model behaviour on different time-scales; explicitly model short-term behavioral policies and transitions between behaviours
* ICF: indepent controllable features; a model is trying to learn independent parts of the world that it can control; something like an autoencoder but every aspect of the world is modeled explicitly through latent variables
* we build features for objects and separate policites for manipulating those objects
* a lot of models uses latents to optimise likelihood, without segragate them into parts representing different parts of the world
* regularise s.t. different parts of the representation are associated with different parts of the world/actions

## Pushmeet Kohli - Exploring the different paths to achieving disentangled representations
* repr learning - learning a formalism to make certain entities and types of info explicit; transform signals to a form that could be effectively exploited to solve a task
* fc7 from alexnet is useful for a wide variety of tasks, but it is invariant to many transformations, which is undesierable in many other tasks
* disentangling through partially-specified models: we can explcitly partition latents into groups representing different things and than train it on pairs on which those things are different to encourage disentangling
* AIR-like Siddharth et. al. 2017: Disentangle repr through semi-sup gen modelling paper

good properties of a repr:
* aware of scene complexity
* it should have conditional attributes: different object types have different types of attributes; e.g. make and orientation for a car, but joint angles for a human
* it should have collection-specific attributes (this is useful, but can be implemented by instance-specific)
* supports multiple tasks

Lessons from Games and Rendering Engines
* we can use a rendering engine as our generative model to learn a structured latent representation
* learning is not easy since no grads, but we can use a mixture of supervised and reinforcement learning
* this repr is quite high level and useful for different tasks: visual analogies, visual question answering, image captioning etc


## Yoshua Bengio - Priors to help automatically discover and disentangle explanatory factors
Intro:
* dependencies between data are simple when the data is mapped into the right abstract space
* in the right space, inference is simple; can be done with linear models
* What is a good repr? Bengio 2013 review paper
* we need clues, i.e., prior to help us disentangle factors
* we'll talk about controllable factors (causal mechanisms, agents) and the conciousness prior
* encoder interprets data at the high level, decoder combines it back

Controllable Factors:
* some factors correspond to independently controllable aspects of the world; they can be only discovered by acting
* if a thing can be independently controlled, e.g. a particular action can affect this thing and nothing else, then they are good candidates for abstraction; it connects with the notion of objects or agents; there is also some spatial consistency to them, but it cannot be separated from other properties
* mirror neurons mimick other people acting in the real world: it's similar to the paper that I've just seen which uses a smoothing distribution of state & action to infer a predictive distribution over actions given the state

Conciousness Prior: what's wrong with our unsupervised learning objectives?
* relationships in the abstract space should be simple, but our training objectives are not talking what's going on in the abstract space, but they focus on the pixel space (likelihood)
* more bits in the data are low-level details do not matter for interpretation
* e.g. modelling p(acoustics) is much worse than modelling p(acoustics|phonemes)p(phonemes), since phonemes contain a lot less noise than the acoustic signal and is more amenable to modelling; phonemes are a sort of an abstract representation of acoustics
* concious thoughts are a composition of just a few selective factors (compared to the full state of the brain)
* yet they have very high predictive value/usefulness for planning
* we have two levels of representation: an unconciouss state and a conciouss one, which is created by attending to parts of the unconcious state; it's a conciouss prediction over attended variables A (soft attention)
* to do this, we need some objective function; ideally something in the abstract space that would not require reconstruction; sth that could e.g. maximise the entropy of the code (amoutn of info), or its predictivue usefulness for actions
* abstract factors are not neurons: number of concepts to think about is combinatorial in the number of expressable things
* factors should be used for long-term prediction; it's not only for t+1 or at a particular time, but it should be stored as a key-value pair that can be used when something relevant happens later
*



# Notes
* learning likelihoods: Learning Implicit Deep Hierarchical Models by Dustin Tran
* make a note on learning ddisentanglement by centering prior for t at latents at t-1: if we do that, things that do not change in the image should have KL very close to zero, while KL for changing things like point of view, orientation or position should change; this way, we could disentangle semantic from position/orientation/illumination and maybe levrage that... interesting :)
* is inductive bias a prior? convolution is a form of an inductive bias (locality and smoothness, the latter if weights are not too big), but it's not a prior in the bayesian sense; inductive bias seems to be a broader concept, a prior, and especially a bayesian one, is just one form of imposing an inductive bias
* we can create structured likelihoods, e.g. renderers, for images, but no schema like that exists for different types of data e.g. smart city or dna; in this case, learning the functional form of likelihood is still applicable; this ties more broadly into the likelihood-free inference stream of thought and I think we could explore it a bit more...
