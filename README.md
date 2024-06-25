# LTTSVABrazil
Details of Bayesian Structural Poisson model of Long Temporal Trend and Seasonal Variation Analysis of Forest Fire Foci in Brazilian Biomes: A Stochastic Approach.

We fitted to data a Structural Poisson model used in similar studies (Villar-Hernández et al., 2022; Costafreda, 2017). The random variable $Y_t$ that represents the number of fires at a given time $t$ (month) for a specific biome, can take values $y_t  = 0,1,2,…,$ and so on. The external covariates in our analysis were the following meteorological variables: maximum and minimum monthly temperature (Tmax and Tmin, respectively, measured in Celsius), average monthly wind speed (WS, measured in $ms^(-1)$), monthly precipitation ($P$, measured in mm), and monthly evaporation ($ETo$, measured in mm).

The following two equations form the foundation of our modeling approach:
	$Y_t |\lambda_t \sim Po(\lambda_t ),t=1,2,…,$

	$\ln⁡(\lambda_t)=x_t^T \beta+m_t+s_t+u_t$

Where:

+ $Po$ denoted the Poisson distribution,
+ $\lambda_t$ is the rate parameter that represent the expected number of fire focis at time $t$. 

We link $\lambda_t$ to the linear predictors using the canonical link function, as shown in equation 2. In this equation, $x_t^T$ represents the vector of standardized environmental covariates (by subtracting the mean and dividing by the standard deviation). The vector $\beta$ corresponds to the regression coefficients.

The structural component of our model consists of two parts: $m_t$, which represents the latent trend (long-term variation), and $s_t$, representing the seasonal variation. Additionally, the term $u_t$ represents the unstructured random component, also known as the error term. The latent trend in our model was captured using a random walk of order one, expressed as $m_t=m_(t-1)+\epsilon_{1t}$. Here, $\epsilon_{1t}$ is assumed to follow a normal distribution, $\epsilon_{1t}  ~ N(0,\sigma_{slope}^2)$, where $\sigma_{slope}^2$ represents the variance of the slope component.

To account for seasonal variation with a periodicity of $s=12$ (representing 12 months), we used the formulation $s_t=-\sum_(j=1)^11 (s_(t-j)+\epsilon_{2t})$. The term $\epsilon_{2t}$ follows a normal distribution, ε_2t  ~N(0,σ_seasonal^2), with σ_seasonal^2 representing the variance of the seasonal component. Finally, the unstructured term, u_t, is assumed to be independently and identically distributed according to a normal distribution, u_t  ~ N(0,σ_u^2).
It's important to note that the formulation of ln(λ_t) allows for great flexibility in modeling non-linearities in the trend component while capturing the dependency between successive observations of the response variable.
We fitted the aforementioned model from a Bayesian perspective using the Integrated Nested Laplace Approximation (INLA) methodology (Rue et al., 2009) implemented in the R programming language (R Core Team, 2022). The following priors and hyperpriors were used in the model: β_j  ~ N(0,1000) for j = 1,2,...,6 (indicating diffuse Gaussian priors), σ_slope^2  ~ IG(1,0.00005), σ_seasonal^2  ~ IG(1,0.00005), and σ_u^2  ~ IG(1,0.00005). The parameter values for the inverse gamma (IG) priors were chosen based on the recommendations by Blangiardo and Cameletti (2015).
![image](https://github.com/bjesusvh/LTTSVABrazil/assets/6344854/7fe56d97-0d5c-445e-8583-d41255ca8c18)
