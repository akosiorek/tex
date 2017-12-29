
### Kalman VAEs #176
* locally linear transition across timesteps: exact Kalman filter inference

###
* proximal GD is a generalisation of gradient descent to non-smooth case

## DL and RL track 14:50

### Imagination-Augmented RL #139
* RL doesn't generalise too well and is expensive to train
* in high dim, models are costly and inaccurate
* combine model-based and model-free aspects, DYNA-like
* Agent queries an enviornment model when necessary and the enviornment gives an answer; the agent learns to interpret the answer
* the model is any sequential model (RNN)
* agent can be whatever, e.g. value function or a dqn
* model is learned unsuervised; agent is learn by rl, but the way the agent chooses the action is fixed (MC-rollout and max-expected reward action)
Model:
* encode one imagination-rollout for each possible action
* compute and encode a model-free path by unrolling the policy
* pass codes of both to the final policy which combines the above
* there's also a distilation stage, which distills the slow thinking of I2A to a quick model-free policy
* planning is learnt implicitly by reward maximisation

## Spotlights

### Dual Path Networks #130
* ResNet is like an MLP but with shared connections
* ResNet resuse features across layers, while MLPs keeps exploring new features and builds hierarchies, but might have a lot of feature redundancies since some featurs can be required at multiple levels
* Each block has two outputs, one is passed into a residual path, the other is fed into the next layer
* less computation, less memory, higher accuracy on imagenet

### Relational Networks
* CNNs and RNNs are biased to consider relations between objects that are proximal in space and time, respectively
* RNs are permutation invariant; extract "objects" and consider all of them pairwise; feed pairwise description into a small MLP and add activations.

### Scalable Trust-region method for DRL using Kornecher-factored approx #140
* use natural gradients for better sample efficiency
* K-FAC: kronecker-factor approximated curvature
* kronecker product of two small matrices to approx Fisher info matrix
* define the Fisher matrix, apply K-FAC approx
* use natural policy gradient with the above

### Attention is all you need: the transformer
* attention over sequences for any seq2seq
* attention in encoder-decoder seq2seq models

### Learning Combinatorial Optimization over Graphs
* exact is intractable, heuristics work only in some cases
* in many applications, the same problem is solved multiplie times with slightly different data, e.g. social networks
* use RL to learn an agent able to solve a task
* negative reward per timestep -> minimum num of timesteps
* not sure how to repr the value funciton: use structure2vec embedding
* max cut, tsp, etc, quite good

### Uncertainty Quantification in DL by Balaji...
*

# Thursday

## Deep Learning 11:10

### Masked Autoregressive Flow
* really good counterpart to IAF; IAF is fast to sample from but slow to estimate p(x), MAF is fast to estimate p(x) but slow to sample from

### DeepSets

### From Bayesian Deep Learning to Rnns? <--- READ!!!!
* building a bridge between multi-loop iterative algos and multi-scale RNNs
* avoid local minima, converge to global minima more quickly
* maximally sparse estimation is touched by local minima a lot
* iterative thresholding is NP hard, because there is combinatorially many combinations of non-zero values that lead to a lot of local minima
* trainanble neural net analogue
* Simple RNN looks just like Iterative Hard Thresholding with hardcrafting weights
* can we learn an improved version of IHT?
* there are no combinations of weights that handle strong correlations well; the solution is to start with sth that can do that and go form there
* Sparse Bayesian Learning usies type-2 ML and is handle covariances
* SBL does not admit simple iterative impl; requires multi-loop which is amenable to RNNs
* in SBL sparsity shifts from x to the covariance matrix, from which sparsity transfers into x, which is crucial for RNN impl
* SBL can be implemented as a modified LSTM with different nonlinearities, but it permits only a single iteration of the inner loop; while it is ok, we can do better by doing more iterations of the inner loop
* multi-iteration activations resamble multi-scale RNNs, e.g. clockwork RNNs
* training is slow but test-time inference is fast

### Self-Normalising NNs
* turn the alchemy of batch-norm into electricity

### Batch Renormalisation <--- READ
* extenstion to batch-norm
* normalising a minibatch introduces variance and bias, can hurt the model if examples are correlated or model small
* batch renorm corrects the bias
* training normalisation is a biased estimator of inference normalisation
* if samples in a minibatch are correlated, we are injecting info into training that are absent at inference; e.g. when all samples come from the same class, the activations depend on the minibatch but also on the class-conditional mean activation, which injects info about the class; interesting
* renomalise training activations by the full-batch moments as used at inference time
* there's a slight performance improvement, which grows to a dramatic one in case of non-idd samples in the minibatch
* implemented in TF


### Nonlinear Random Matrix Theory for Deep Learning
* complex systems are often well modeled by random vars
* matrices in NNs start off as random as well
* matrix structure is very important: evecs and evals
* let's look at matrices of post-activations?
* they evaluate spectra of random matrices in NNs, might be interesting

### Spherical Convs and apps in molecular modelling
*
