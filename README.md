# gaia-completeness-ml-demonstration
A simple repo demonstrating how one can use a neural network to model the completeness of a sub-sample of Gaia.

# Description of the problem
Modeling the completeness of a sub-sample is equivalent to predicting the probability that a star in the Gaia catalogue is part of the selected sub-sample. This is equivalent to a binary classification problem where our training set consists of stars that are part of the sub-sample (label 1) or not (label 0). Completeness is then equivalent to the probability that the star has label 1.

Binary classification is a [well-studied problem](https://en.wikipedia.org/wiki/Binary_classification). The most common approach in astronomical context is to bin the stars along various important dimensions such as longitude, latitude, apparent magnitude, or colour, and then output the average value within each bin. This however doesn't generalize too well to higher dimensional feature space, and it also doesn't provide a continuous representation of the completeness. This notebook presents a different approach where we model the completeness using a neural network. The notebook mainly serves as a proof of concept, so we use a simple fully connected neural network with a sigmoid function as the final layer, and an appropriately chosen L2 regularization. We demonstrate the performance on a dataset of all Gaia DR3 stars with $G < 14.5\mathrm{\ mag}$ and within a square field of view with galactic longitudes $-20^\circ < l < 10^\circ$ and latitudes $-10^\circ < b < 20^\circ$. We choose the sub-sample of interest to be stars with radial velocity measurements and some quality cuts.

To highlight some of the short-comings of the method, neural networks are really flexible for modeling higher-dimensional data, but they're more difficult to fine tune. Depending on the complexity of the data, one has to choose suitable hyperparameters (number of hidden layers, neurons per layer, regularization etc.). Also, one should make sure there are no systematic biases which could feasibly occur for example in volumes of high or low densities or density gradients.