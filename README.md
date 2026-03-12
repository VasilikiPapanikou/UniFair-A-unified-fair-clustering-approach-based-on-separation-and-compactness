# UniFair: A Unified fair clustering approach based on separation and compactness.
Clustering is increasingly used to support high-impact de-
cisions, yet standard objectives such as k-means can produce cluster-
ings that treat demographic groups unequally. Existing fair clustering
methods typically optimize a single notion of fairness and often overlook
how clustering costs interact with the geometry of the induced deci-
sion boundaries. We propose UniFair, a unified framework that jointly
optimizes separation fairness and social fairness. Separation fairness en-
courages protected groups to lie farther from the induced decision bound-
aries, while social fairness reduces disparities in within-cluster distortion
by penalizing group-wise clustering costs. We develop gradient-based op-
timization procedures for separation-fair and unified k-means objectives,
and extend them to deep clustering by enforcing the same criteria in
the latent space of an autoencoder. Experiments on tabular and image
datasets show that UniFair reduces both boundary-related and cost-
based group disparities with only a modest increase in clustering loss.


This repository provides implementations of multiple fairness-aware 
clustering algorithms for high-dimensional tabular data. These methods 
extend classical k-means by incorporating fairness constraints derived 
from demographic groups and counterfactual reasoning.

The repository includes:

1. Separation Fair k-Means
2. Socially Fair k-Means
3. Unifair k-Means (combined method)
4. Deep Separation, Deep Social & Deep Unifair Fair k-Means

Each method addresses fairness in clustering from a different 
perspective, and all are implemented in a modular and reproducible form.

--------------------------------------------------------------------
## Separation Fair k-Means
--------------------------------------------------------------------

Separation Fair k-means enforces fairness by requiring that demographic 
groups remain equally well separated from cluster decision boundaries.

The method measures fairness using *counterfactual hyperplane distance*:
it computes, for each point, the squared signed distance to the 
mid-hyperplane between its closest two centroids. If the two demographic 
groups have significantly different average distances, the clustering 
is considered unfair.

The algorithm penalizes large differences between groups, ensuring that 
both subgroups are positioned at similar levels of separation from 
cluster boundaries. This reduces the risk of systematically placing one 
group near ambiguous regions of the space.

--------------------------------------------------------------------
## Socially Fair k-Means
--------------------------------------------------------------------

Socially Fair k-means enforces fairness by encouraging each cluster to 
represent demographic groups proportionally to how they appear in the 
dataset.

The method computes how each demographic group is distributed *inside* 
every cluster and penalizes cases where one group is consistently placed 
farther from its centroid than the other. Intuitively, this prevents 
clusters from being biased toward one demographic group at the expense 
of another.

This method ensures that cluster centers faithfully represent both 
groups, promoting balanced and socially fair cluster assignments.

--------------------------------------------------------------------
## Unifair k-Means (Combined Method)
--------------------------------------------------------------------

This algorithm combines the two fairness notions above.

The goal is to simultaneously enforce:
- **Separation fairness** (equal distance from decision boundaries)
- **Socially fairness** (equal representation within clusters)

The method optimizes a joint objective that integrates:
- k-means clustering quality,
- fairness based on boundary separation, and
- fairness based on demographic representation.

This leads to clusterings that are both structurally fair (in decision
geometry) and socially fair (in demographic distribution).

--------------------------------------------------------------------
## Deep Fair Clustering (Deep Separation, Deep Social & Deep Unifair Fair k-Means)
--------------------------------------------------------------------

The deep versions extend the fairness models by incorporating a neural 
network encoder (autoencoder). The encoder learns a nonlinear latent 
representation of the data, and the fairness-aware clustering objective 
is applied inside the learned latent space.

These models allow:
- better handling of nonlinear cluster structures,
- improved robustness on high-dimensional datasets,
- an end-to-end differentiable fairness-aware clustering pipeline.

Both fairness mechanisms (separation fairness and social fairness) can 
be activated in the deep setting.

--------------------------------------------------------------------
### Included Datasets
--------------------------------------------------------------------

The repository supports the following datasets:

- **Adult Income**
- **Credit Card Clients**
- **Student Performance**
- **Bank Marketing**
- **MNIST-USPS**
- **Color Reverse MNIST-USPS**

Each dataset includes a binary sensitive attribute (e.g., gender).  
The code automatically handles preprocessing and scaling.
