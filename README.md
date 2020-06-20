
# Delustering to Improve Preferential Sampling

This work has been published by **Mehdi Rezvandehy** and **Clayton V. Deutsch** at Journal of [Stochastic Environmental Research and Risk Assessment](https://doi.org/10.1007/s00477-017-1388-x) https://doi.org/10.1007/s00477-017-1388-x. **Python** implementation of declustering is presented in this repository. If you have any question about the approach and implementation, please email me at [Mehdi Rezvandehy](rezvande@ualberta.ca).

# Abstract

**The spatial correlation called variogram is a key parameter for geostatistical estimation and simulation. Preferential sampling may bias the spatial structure and often leads to noisy and unreliable variograms. A novel technique is proposed to weight variogram pairs in order to compensate for preferential or clustered sampling. Weighting the variogram pairs by global kriging of the quadratic differences between the tail and head values gives each pair the appropriate weight, removes noise and minimizes artifacts in the experimental variogram. Moreover, variogram uncertainty could be computed by this technique. The required covariance between the pairs going into variogram calculation, is a fourth order covariance that must be calculated by second order moments.**

# Introduction

Geostatistical modeling is widely used to estimate and simulate properties in the petroleum and mining industries. One of the key parameters for geostatistical modeling of continuous variables is the variogram or covariance function for each property. Variogram modeling is performed to fit a model to a sample variogram computed from the data: experimental variogram points are not directly used in geostatistical modeling since the variogram function is required for all distances and they must be positive definite. The variogram model (fitted model) can be attained manually or by applying an algorithm (used in autofiting software) to achieve the optimum fitted variogram model. One conventional approach of auto variogram modeling is measuring the goodness of fit by an objective function, which is the sum of the squared difference between the experimental variogram and the modeled variogram. Random changes to the variogram model that decrease the objective function are accepted. This process is repeated many times (say more than 10000) to obtain the best fitted variogram model with the minimum objective function. Variogram modeling is not the aim of this study.

In practice, variogram modeling is suboptimal in presence of irregular and preferential positioning of the wells. Based on geological and geophysical information data, the data are likely located in the areas of higher quality that would be developed first or that would maximize production. Higher valued areas are also more variable, thus, equal-weighted experimental variograms are often noisy and biased. Weighting the data by declustering techniques compensates for the geometric configuration of the data locations and corrects the statistics; however, this approach is not normally considered in variogram calculation where equal weights are often considered for the variogram pairs. 
**Figure 1**-a shows a synthetic example of clustered well locations in areas of high quality, and sketch of its corresponding variogram for azimuth 0 (b). The variogram is unstable and has fluctuations because for the short lag distance (lag distance h1 in a) the majority of pairs are located in the high quality area with greater variability, and for a larger distance (lag distance h2 in a) the majority of pairs are located in low quality areas. This unbalanced number of pairs within low and high quality areas leads to a noisy variogram due to the fact that the equal weighted averaging as in Equation above does not account for preferential sampling.

<img src="./Images/fig_1.png" alt="drawing" width="800"/>

**Figure1**: *a) Synthetic example of clustered locations in areas of high quality (the center right of the sketch). b) Sketch of experimental variogram for azimuth 0. The noisy and unreliable variogram is due to clustering some variogram pairs in high valued areas.*
 
## Proposed Workflow
The objective of variogram declustering is to correct the effect of preferential sampling. This work proposes a novel approach for variogram declustering. A methodology is proposed to derive declustering weights of variogram pairs that best compensate for preferential sampling; it has three steps: 1) Experimental variogram of the data is calculated and a theoretical model is fitted. The fitted variogram model is used for computing fourth order covariance matrix between variogram pairs. 2) Variogram pairs of each lag distance are assembled from the data. 3) Global kriging is applied on the variogram pairs of each lag distance separately. The declustered variogram is then fit again and used for geostatistical modeling (See **Figure 2**).


<img src="./Images/fig_2.png" alt="drawing" width="800"/>

**Figure 2:** *a) Schematic illustration of variogram declustering by global kriging. a) A variogram model is fitted to the experimental variogram of data. b) Draw variogram pairs of each lag distance from the data. c) Apply global kriging for variogram pairs of each lag distance to improve and decluster noisy variogram.*
