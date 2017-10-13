

I am going to work on AGI. That's what I am interested in, what I believe can happen in future and what I think is worth working on. Working on applications as well as statistical machine learning is important in that in provides tools for solving real-world problems and enriches the language we can use to express models. I believe that AGI is different, however.

I believe that AGI is about reasoning, unsupervised learning and coming up with self-supervised learning signals, something like internal motivation and verification. What do I mean?

Reasoning:
An ability to use available tools to come up with and refine solutions to emerging problems. I feel that for reasoning we need well-functioning lower-level modules, that could be combined to solve more complicated problems. They could be refined while learning to reason, but they have to be available in the first place. RL is also a major part, since it allows working with sparse rewards as they appear in the real world.

Unsupervised Learning:
A lot of what we learn is unsupervised; Before we take any action we typically have ideas of what the consequences are going to be, and we correct our internal models when predicted consequences do not match our intended ones. This is a slow process (people don't change?), but nevertheless possible. I see it as an instance of predictive learning with strong priors on sparsity and consistency.

Self-supervised Learning:
It is strongly tied to the above concepts. Once we can reason, we can predict a consequence of a complicated action; perhaps we can predict how different components could contribute to the overall solution. Perhaps we can use outputs of some components to predict behaviour of different components, as there should be some level of redundancy in the system if it is to be robust. Now, the question is: can we tie those dependencies to create a closed feedback loop, that will bootstrap learning? It might lead to a huge amount of drift in the absence of any external inputs. That's where reasoning and RL comes in: Sparse rewards from RL can be used to calibrate the internal feedback process, while leaving the actual learning to continuous and dense internally available error signals.
