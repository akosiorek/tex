1. Temporal VAEs, Predictive Coding, Neuroscience

  * exploit problem structure for prediction
  * eliminate internal covariate shift in the encoder
    * does not address the decoder, by decoding is typically easier than encoding, so shouldn't be a big issue
  * very wide applicability

  Questions:
  * plumbing: How to model dependencies? The model should learn a hierarchical representation, not only error moments.
  * predictive variance: predictive distribution at the beginning might not be well behaved; how to prevent extreme values of variance leading to vanishing or exploding inputs to higher layers?
  * neuroscience: can we get inspiration or hints from neuroscience to reduce the search space?

2. External Memory for Navigation

  GTMM has addressed the problem of using external memory for sequential tasks but used only toy data and only in a *simple* generative scenario
  * huge potential in RL where memory can be used in navigation

  Questions:
  * How to use discrete addressing for write-access
  * How to initialise memory with landmarks
  * How to cue the agent to navigate between landmarks in memory?
  * Can we structure SLAM as an RL task and reuse maps built that way?

3. External Memory for Problem Solving [written before reading Neural Programmer-Interpreter]

  * Can we store subprograms or procedures in memory and reuse them to solve more complicated programs?
  * Can we manually encode subprograms or do they have to be learned?

  * Instead of storing biases, we could store programs defined by transition functions of RNN. A function like that would define a program, together with its length or stopping condition.
  * Stored programs could be learned end-to-end with the controller.

  * Instead of explicitly storing programs, can we have a program meta-model, which given some representation of a problem produces parameters for an RNN-like model to solve it? Like a DFN, but the meta-model would produce new parameters only every once in a while to adapt to the changing (nature of the) task.
    * Similar to a hierarchical RL with options, but the amount of possible sub-programs is very high and it allows interpolation between different modes.
    * Nice for motion generation.
    * Trade-off between constant modulation of the executed program and discrete step-like changes between them:
      * What is more efficient? Which one is more stable? Are different programs interpretable?

  Application:
  Learning motor control primitives and composing them into more complicated movements, like neural movement primitives.

  How's that different from hierarchical RL (options)?
  * we can learn them in a generative setting by trying to imitate mocap data
  * in the simplest case it'd be a trainable lookup table
  * in a more general case: transition parameters or a motion embedding

  Questions Problems with the NPI:
  * Requires complete execution traces for learning; We can teach it only tasks that we know how to solve ourselves
  * Can we learn high- and mid-level programs that execute low-level ones by RL, without full execution traces?
  * Once the controller is learned, can we learn program embeddings without execution traces? E.g. we could train a learning-to-learn model to produce known embeddings from known input-output pairs for those programs and then create embeddings for input-output pairs of unknown programs and train by RL.


4. Unsupervised Object Tracking: Generative Temporal Model with Attention
* Extend AIR for sequences: Work in Progress

5. Task-dependent Latent Representation

  Latent representation can be viewed as an abstract description of the scene.
  * It should be minimal (no noise, distractors) and yet specific to the task at hand.
  * It should have a form that simplifies execution of the task.

  Examples:
  * Global representation (a single vector) for scene classification, state value estimation, navigation
  * Local representation for object tracking, object classification
  * Multiple local representations for object detection, relational reasoning, perhaps navigation

  Variable-length variable-resolution representation allows superior resource allocation and explicit multi-step reasoning about parts of the scene.

  Applications:
  * Assembly tasks in RL
  * Logic games, puzzles
  * Multiple object tracking and detection
  * Relational Reasoning


6. Spatially Organised Memory

  Current addressing schemes lead to independent memory entries; DNC solves it by introducing temporal connections between cell, thus making them temporally correlated. Some tasks, like navigation, could use spatially correlated memories and tailored lookup methods

Generally:
  VI & Sampling > Statistical ML and DL > RL or anything else
    * State-space models
    * Better posteriors
    * Sampling with VI
    * O(1) uncertainty estimation

  Attention & Memory > General DL
    * Combining Attention, Memory and Temporal Reasoning for self-supervision -> Consistency
    * Motion estimation, physics, environment simulators

  Small Components > Big Systems
    * Relation Nets > Interaction Nets

  Principled Research > Trial and Error
    * Can we interpret properties mathematically and then improve maths to improve properties?

  Interpretability > Complexity
    * KL in VI
    * Emergent behaviour
