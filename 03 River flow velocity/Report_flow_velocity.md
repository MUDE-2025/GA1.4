# Report for Group Assignment 1.4, Flow velocity Dataset

*[CEGM1000 MUDE](http://mude.citg.tudelft.nl/): Week 1.4, Friday, Sept 26th, 2025.*

_Remember to read the grading and submission instructions in the `README.md` file thoroughly before finalizing your answers in this document!_

## Questions

**Question 1**

Give a short description of the provided dataset in statistical terms, based on the tasks in the notebook. Visualize the data and choose a parametric distribution function for each variable between the indicated ones: choose between a **lognormal** and **uniform** distribution to model the water depth $h$, and between a **Gaussian** and **Gumbel** distribution for the flow rate $q$. Justify your choice based on the previous description and visualization. 

_You should describe your data with only a few sentences, and be sure to use quantitative information! Refer to that description to choose the parametric distribution function. You can also include some plots that may support your reasoning._

_Distribution chosen for **<VARIABLE_1>**:_ **your distribution here.**

_Your justification here._

_Distribution chosen for **<VARIABLE_2>**:_ **your distribution here.**

_Your justification here._

% solution_start

- $h$ and $q$ have a similar mean, but $h$ has significantly lower variance. To compare the variability of variables with different magnitudes, it can be useful to compute the <b>coefficient of variation</b>, which normalizes the standard deviation against the mean. If we do so, we obtain $CV(h)=\sigma/\mu=\sqrt{0.000539}/3.402 = 0.007$ and $CV(q)=\sigma/\mu= \sqrt{6.718}/8.657 = 0.299$. Thus, $q$ has significantly higher variability than $h$.
- Both $h$ and $q$ have a positive non-zero skewness, with the one for $q$ being significantly higher. Thus, the data presents a right tail and mode < median < mean. An appropriate distribution for $h$ and $q$ would be one which: (1) it is bounded in 0 (no negative values of $h$ or $q$ are physically possible), and (2) has a positive tail. If we consider the distributions that you have been introduced to, Lognormal, Gumbel or Exponential distributions would be a possibility.

$h$: Lognormal - Reasoning: This distribution is clearly not uniform, and the positive skewness suggests we need a right-tailed distribution.

$q$: Gumbel - Reasoning: This distribution has a clear right tail, so a symmetric distribution like the Gaussian is not an option. Be aware that both the Gaussian and Gumbel distributions are unbounded, which may enter permit impossible negative values.

% solution_end

% solution_start

Rubric: - 3 points in total

    1 point for recognizing that $q$ has a higher variability than $h$
    0.5 points for each correct distribution
    0.5 points for each correct justification

% solution_end

**Question 2**

Fit and assess the goodness of fit of the selected parametric distribution functions to the dataset. Use (at least) Kolmogorov-Smirnov test and one graphical technique. For the graphical technique, choose between the QQplot and logscale plot. Describe in a few sentences how the chosen parametric distribution functions performs.

_Remember to use quantitative information based on the goodness of fit metrics that you have used. Also, you can include some examples of the differences in the computed and observed non-exceedance probabilities._

% solution_start

- <b>Logscale plot</b>: This technique allows to visually assess the fitting of the parametric distribution to the tail of the empirical distribution. For $h$ and $q$, the lognormal and Gumbel distribution does not agree with the empirical distribution in the right tail very well. In both cases, high values start to slightly deviate from the empirical distribution, indicating that for lower non-exceedance probabilities it might not be a good fit. </li>
- <b>QQ plot</b>: Similar conclusions to those for Logscale can be derived. Here, we can also see that both distributions deviate slightly in the left tail, too.
- <b>Kolmogorov-Smirnov test</b>: remember that the test statistic measures the difference between two distributions. The p-value then represents the probability of observing a difference at least that large for a sample from the assumed distribution. If p-value is lower than the significance ($\alpha=0.05$, for instance), the null hypothesis is rejected. Considering here $\alpha=0.05$, we can reject the hypothesis that the variable $h$ comes from a lognormal distribution and that $q$ comes from a Gumbel distribution.

% solution_end

% solution_start

Rubric: - 3 points in total

    1 point for recognizing that both distributions have similarly good fits, but deviate in the tails (0.5 points for a convincing explanation that deviates from that) in the graphical logscale or QQ plot
    0.5 points for the correct KS p-value for $F$ (0.0) or for the correct computation if they chose a different pdf 
    0.5 points for the correct KS p-value for $v$ (0.0) or for the correct computation if they chose a different pdf
    0.5 points for the correct interpretation of the KS results for $F$: we can reject H_0
    0.5 points for the correct interpretation of the KS results for $v$: we can reject H_0
 
% solution_end

**Question 3**

Propagate the uncertainty through the equation to estimate the flow velocity, $u$, using both observations and simulated samples. Provide a bulleted list that summarizes differences between the two obtained distributions.

- your
- bulleted
- list
- here

Compare the simulated samples and observations $(q,h)$ in a scatter plot, then prepare a bulleted list that describes the differences. Is there anything you could improve in the analysis? Provide with recommendations to improve the performed analysis. They can be both about the univariate distributions and about the propagation of uncertainty method you have used.

_Include your figure here. Be sure to use high contrast data symbols/colors and a legend to differentiate the two data sets clearly._

% solution_start

- In the PDF plot, we can see that the shape of the distribution is similar for $u$. In the CDF plot, we can see that there are significant differences in the tail of the distribution of $u$. Specifically, the values from the observations are lower than those computed from the simulations. This is because the both distributions overestimated the exceedance probability in the right tails, also leading to larger predictions of the flow velocity.
- <b>Disadvantages:</b> we are assuming that $h$ and $q$ are independent (we will see how to address this issue next week). But is that true? Also, the results are conditioned to how good model is the selected parametric distribution. In this case, since the tail of the distribution of $h$ is not properly fitted, the obtained distribution for $u$ deviates from the one obtained from the observations.
- <b>Advantages:</b> I can draw all the samples I want allowing the computation of events I have not observed yet (extreme events).
- The observations along a narrow drop-shaped area of the plot, whereas the simulations are spreaded all around. This is because the observations are dependent, since there is a physical relationship between the water depth and the velocity of the flow, while the simualtions were assumed to be independent.
- <b>Some suggestions:</b> Improve the fit in the tail for $h$ and $q$. Account for the dependence between the two variables.

% solution_end

% solution_start

Rubric: - 4 points in total

    1 point for recognizing the similarity between the observed and simulated distribution for $u$ (similar spread, similar mode.); partial points for vague or unconvincing explanations
    1 point for recognizing the difference between the observed and simulated distribution for $u$ (slight deviation in the tail); partial points for vague or unconvincing explanations
    1 point for recognizing that there is a relationship in the observations that the simulation does not capture
    1 point for making reasonable suggestions for improvements (capturing the dependency, truncating unphysical values, etc.)
    (half points for slight deviations)
 
% solution_end
**Last Question: How did things go? (Optional)**

_Use this space to let us know if you ran into any challenges while working on this GA, and if you have any feedback to report._

**End of file.**

<span style="font-size: 75%">
*Copyright 2025 <a rel="MUDE" href="http://mude.citg.tudelft.nl/">MUDE</a>, TU Delft. This work is licensed under <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">CC BY 4.0</a>.*