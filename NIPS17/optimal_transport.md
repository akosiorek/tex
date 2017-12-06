# Optimal Transport

## Learning with a Wasserstein Loss
How W-dist is useful to learn generative model?

v_data = average dirac_x <- empirical data pdf

MLE - requires a fmaily of distributions that is positive at every possible point; otherwise you get numerical instabilities since log0 = -inf

MLE - fit a blob p_theta to v_data by maximising likelihood; but p_thetra has to be non-zero everywhere

Otherwise, we can parametrise the data space by low dim latent space and transform into a higher dim data space by push-forward:

find theta such that f_theta \cdot \mu is close to the data distribution; this obviously doesn't work because the push-forward distribution is zero in most places

=> use a richer metric for measures, one that can handle measures with non-overlapping supports

min_{\theta \in \Theta} metric(v_data, p_theta)
-> other divergences instread of ML, e.g. chi-sqiared, Kantorovich, Hellinger distances


### Min Kantorovich distance
Minimise W-dist between data v_data and p_theta

-> use a neural net to estimate W-distance and its gradient;
e.g. W-GAN approxes the dual form of the Kantorovich problem

new paper from T Salimans - nns for the iterative scheme

https://optimaltransport.github.io
