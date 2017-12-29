# Metalearning Symposium

I arrived late; I was at the kind-of-intelligence symposium but it is very high-level and, although interesting, it's enough to spend a bit reading. Here I might actually learn/understand something. And I learned that Demis is real yesterday so I don't need to actually see him.

## Neural Plasticity? K. Stanley
* plastic neural nets learn to navigate mazes better than non-plastic ones and can re-learn on the fly if we e.g. start putting reward in a different place

## PathNet and Beyond - Chrisantha Fernando
1) start
* at the beginning nobody believed in evolutional learning in DeepMind, so he experimented with evolution itself for a year :)
* very small neural networks with <20 neurons to control cheetach or drive a car in a game

2) evolution vs gradient descent

3) combination of evolution and GD
* currently everyone trains a separate neural net; wouldn't it be nice if we all trained the same net, though?
* we can split every layer in a big model into separate modules and then choose some modules from every layers
* modules are combined by adding the outputs of each module
* that way, we construct directed acyclic graphs through the network: each DAG defines a path, which can be seen as a view of model parameters
* we can have several tasks using different modules or several workers training the same task and having a separate path
* every K iterations, worker can adapt the best path from other workers and mutate it a bit, hence evolution

## Bayesian Opt for Automated Model Selection
* bayesian opt = actitive learning, in the sense that obtaining data is expensive and the number of queries should be minimised
* vision: automated active learning, so that no ML expert is needed to design the active learning pipeline, including the ML model in the pipeline
* use a dynamic bag of models and prune model/model types as learning progresses
* Bayesian opt uses a model, typically a GP to learn the expected utility as a function of the param space
* we learn the GP by maximising the utility function?
* we can compare the models in the model bag by model evidence; model evidence is the likelihood of the model generating the data, averaged over the posterior distrib of model parameters
* frame model search as an optimisation problem

Why is this a hard problem?
* model evidence function is highly complex and generally intractable; even estimation is very expensive
* even seemingly similar models offer vastly different data explanations
* model similarity depends on geometry of the data

Overview of Bayes Opt:
* we have an expensive to evaluate, gradient-free, nonlinear objective function defined on a discrete support: ideal case for Bayes Opt
* we need an informative prior: a GP with a mean function and a covariance function that are defined for different models
* we need a "mean mean" and "cov cov" function defined by a "kernel kernel", because model evidence is defined from a model, which is defined over data (if we use GPs as our models for both bayes opt and the actual task)

## Automatic Machine Learning and How to Speed It Up - Frank Hutter uni Freiburg
* bayes opt is typically quite slow at the beginning, since it has to explore the param space, but it tends to speed up as more information is gathered, nice; sometimes is "only" two times faster overall than random search, but it's still quite good
* autosklearn: automatic fitting of different classifiers in sklearn via bayes opt :D <-- give it a go!!!!!!!!!!!!!!!!!!!!
* 
