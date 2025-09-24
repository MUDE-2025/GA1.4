# Report for Group Assignment 1.4, Traffic Dataset

*[CEGM1000 MUDE](http://mude.citg.tudelft.nl/): Week 1.4, Friday, Sept 26th, 2025.*

_Remember to read the grading and submission instructions in the `README.md` file thoroughly before finalizing your answers in this document!_

## Questions

**Question 1**

Give a short description of the provided dataset in statistical terms, based on the tasks in the notebook. Visualize the data and choose a parametric distribution function for each variable between the indicated ones: choose between a **lognormal** and **exponential** distribution to model the vehicle flow, and between a **Gaussian** and **Gumbel** distribution for the average velocity. Justify your choice based on the previous description and visualization. 

_You should describe your data with only a few sentences, and be sure to use quantitative information! Refer to that description to choose the parametric distribution function. You can also include some plots that may support your reasoning._

_Distribution chosen for **<VARIABLE_1>**:_ **your distribution here.**

_Your justification here._

_Distribution chosen for **<VARIABLE_2>**:_ **your distribution here.**

_Your justification here._

% solution_start

- $F$ features a higher mean but also a significantly higher variance. To compare the variability of variables with different magnitudes, it can be useful to compute the <b>coefficient of variation</b>, which normalizes the standard deviation against the mean. If we do so, we obtain $CV(F)=\sigma/\mu=\sqrt{531318.298}/923.655 = 0.789$ and $CV(v)=\sigma/\mu = \sqrt{6.839}/80.140 = 0.033$. Thus, $F$ has far higher variability than $v$.</li>
- $F$ has a weak positive skewness, and $v$ has negative skewness. An appropriate distribution for $F$ might be one that features a right tail, such as a right-tailed Gumbel, beta, exponential, or lognormal distribution. For $v$, we might want to consider a left-tailed distribution, for example a beta or left-tailed Gumbel distribution.

$F$: exponential, although any fit is horrible. Perkele. - Reason: the distribution has strong positive skewness, indicating a right tail, and mean of the distribution is very close to the left bound.

$v$: left-tailed Gumbel - Reason: the distribution has a negative skewness, so a symmetric distribution like a Gaussian would not be a good fit. The left-tailed Gumbel distribution fits our needs better.

% solution_end

% solution_start

Rubric: - 3 points in total

    1 point for recognizing that $F$ has a higher variability than $v$
    0.5 points for each correct distribution
    0.5 points for each correct justification

% solution_end

**Question 2**

Fit and assess the goodness of fit of the selected parametric distribution functions to the dataset. Use (at least) Kolmogorov-Smirnov test and one graphical technique. For the graphical technique, choose between the QQplot and logscale plot. Describe in a few sentences how the chosen parametric distribution functions performs.

_Remember to use quantitative information based on the goodness of fit metrics that you have used. Also, you can include some examples of the differences in the computed and observed non-exceedance probabilities._

% solution_start

- <b>Logscale plot</b>: This technique allows to visually assess the fitting of the parametric distribution to the tail of the empirical distribution. We can see that both distributions don't fit the right tail terribly well: the exponential distribution overestimates the exceedance probabilities in the right tail for $F$, erring on the side of caution, and the left-tailed Gumbel underestimates the exceedance probabilities in the right tail for $v$. </li>
- <b>QQ plot</b>: The exponential distribution does not capture the distribution in $F$ terribly well. For $v$, the left-tailed Gumbel distribution fits fairly well for most of the datapoints, but it deviates in both the left and right tail.</li>
- <b>Kolmogorov-Smirnov test</b>: remember that the test statistic measures the difference between two distributions. The p-value then represents the probability of observing a difference at least that large for a sample from the assumed distribution. If p-value is lower than the significance ($\alpha=0.05$, for instance), the null hypothesis is rejected. Considering here $\alpha=0.05$, we can reject that the variable $F$ comes from a exponential distribution. However, we cannot reject the hypothesis that $v$ might come from a left-tailed Gumbel distribution.

% solution_end

% solution_start

Rubric: - 3 points in total

    1 point for recognizing that neither distribution fits the tail very well (0.5 points for a convincing explanation that deviates from that) in the graphical logscale or QQ plot
    0.5 points for the correct KS p-value for $F$ (0.0) or for the correct computation if they chose a different pdf 
    0.5 points for the correct KS p-value for $v$ (0.102) or for the correct computation if they chose a different pdf
    0.5 points for the correct interpretation of the KS results for $F$: we can reject H_0
    0.5 points for the correct interpretation of the KS results for $v$: we cannot reject H_0
 
% solution_end

**Question 3**

Propagate the uncertainty through the equation to estimate the traffic density, $D$, using both observations and simulated samples. Provide a bulleted list that summarizes differences between the two obtained distributions.

- your
- bulleted
- list
- here

Compare the simulated samples and observations $(F,v)$ in a scatter plot, then prepare a bulleted list that describes the differences. Is there anything you could improve in the analysis? Provide with recommendations to improve the performed analysis. They can be both about the univariate distributions and about the propagation of uncertainty method you have used.

_Include your figure here. Be sure to use high contrast data symbols/colors and a legend to differentiate the two data sets clearly._

% solution_start

- In the PDF plot, we can see that the computed traffic density does not fit the observed density very well. With the exception of a few outliers, the simulations tend to predict higher traffic densities than we observed, but underestimates the traffic density between 15 and 30 vehicles per km. </li>
- <b>Disadvantages:</b> we are assuming that $F$ and $v$ are independent (we will see how to address this issue next week). But is that true? Since we have sampled $F$ and $v$ independently, there will be simulations where high traffic flow $F$ and high velocities $v$ coincide, resulting in perhaps unrealistically high simulated traffic densities. Also, the results are conditioned to how good of a model the selected parametric distribution is. In this case, since the exponential distribution performs poorly for $F$, the obtained distribution for $D$ also deviates from the one obtained from the observations. <b>Advantages:</b> I can draw all the samples I want allowing the computation of events I have not observed yet (extreme events).
- The observations are focussed in a slightly curvy area of the plot, whereas the simulated values are spread more chaotically. This is because the observations are dependent due to a a practical relationship between the flow of traffic and the average velocity (intuitively, if the traffic flow becomes too large, the average velocities slow; we can observe this in the extremes), while the simulations are assumed to be independent. Moreover, we can see that negative numbers for the number of vehicles are sampled, which do not have a physical meaning. 
- <b>Some suggestions:</b> Improve the fit of $F$ with a mixture distribution. Account for the dependence between the two variables. 

% solution_end

% solution_start

Rubric: - 4 points in total

    2 for recognizing the differences between the observed and simulated distribution for $D$ (simulated is smoother, observed has more kinks, observed has higher mode etc.); partial points for vague or unconvincing explanations
    1 point for recognizing that there is a relationship in the observations that the simulation does not capture
    1 point for making reasonable suggestions for improvements (capturing the dependency, truncating unphysical values, etc.)
    (half points for slight deviations)
 
% solution_end


**Last Question: How did things go? (Optional)**

_Use this space to let us know if you ran into any challenges while working on this GA, and if you have any feedback to report._

**End of file.**

<span style="font-size: 75%">
*Copyright 2025 <a rel="MUDE" href="http://mude.citg.tudelft.nl/">MUDE</a>, TU Delft. This work is licensed under <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">CC BY 4.0</a>.*