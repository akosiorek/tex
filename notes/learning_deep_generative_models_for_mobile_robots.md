MPE inference: Most Probable Explanation inference

* how long will we have to justify using DL? It's obvious that it has superior performance in most cases...
* feels like a GOFAI paper: SVM, Random Forest, Boosting


* universal probabilistic generative model: WTF?
* reads like a piece of folklore

* Use of Sum-Product Networks to jointly model scene geometry and semantic categories
  * A type of a graphical model that admits efficient learning and inference, since it guarantees that factors correspond to simple and normalised probability distributions

* A mixture of networks with randomised architectures
  * Every mixture encodes different set of conditional independence properties between input variables, which is useful because the dependency structure is generally unknown and is here MC-approximated

* Training by a greedy EM approximation
  * Greedy because the expectation is approximated by the maximum likelihood estimate of the posterior
  * The EM is modified in an arbitrary way...


Input: polar occupancy grid from a laser
  * use a particle filter to integrate laser measurements over a short window

* Occupancy grid is sub-divided into "views" that span some part of the grid
* for each view there's a separate SPN
* view-SPNs are combined into a global SPNs, one for each place class
* class-SPNs are combined into a global SPN and represens the class label



Tasks:
* type of scene classification
* outlier or unknown class detection by thresholding probabilities
* generation of prototypical examples for different semantic classes
* conditional inference with evidence: missing value imputation
