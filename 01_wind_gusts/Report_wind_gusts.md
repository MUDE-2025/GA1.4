# Report Wind Gusts Dataset

## Questions

**Question 1**

Give a short description of the provided dataset in statistical terms, based on the tasks in the notebook. Visualize the data and choose a parametric distribution function for each variable between the indicated ones: choose between a **lognormal** and **exponential** distribution to model the wind speed, and between a **Gaussian** and **beta** distribution for the wind gust speed. Justify your choice based on the previous description and visualization. 

_You should describe your data with only a few sentences, and be sure to use quantitative information! Refer to that description to choose the parametric distribution function. You can also include some plots that may support your reasoning._

_Distribution chosen for **<VARIABLE_1>**:_ **your distribution here.**

_Your justification here._

_Distribution chosen for **<VARIABLE_2>**:_ **your distribution here.**

_Your justification here._

% solution_start

- Both variables have similar means (with the mean of $G$ being naturally larger) but different variances. To compare the variability of variables with different magnitudes, it can be useful to compute the **coefficient of variation**, which normalizes the standard deviation against the mean. If we do so, we obtain $CV(v)=\sigma/\mu=\sqrt{1.990}/2.832 = 0.498$ and $CV(G)=\sigma/\mu= \sqrt{10.185}/6.539 = 0.488$. Thus, we can see that $v$ and $G$ have approximately similar variability.
- Both $v$ and $G$ have a positive non-zero skewness, but the one for $v$ is a bit higher. Thus, the data presents a right tail and mode < median < mean. An appropriate distribution for $H$ and $G$ would be one which: (1) is bounded in 0 (no negative values of $H$ or $T$ are physically possible), and (2) has a positive tail. If we consider the distributions that you have been introduced to, the Lognormal, Gumbel, beta, or Exponential distributions would be possibilities.

$v$: lognormal - Reasoning: both distributions have a right tail and a left bound, but the mode of the PDF is not at the left bound. Hence lognormal.

$G$ : beta - Reasoning: the distribution has a positive skewness, indicating that it is not symmetric; furthermore, a Gaussian distribution has no bounds and so may permit unphysical negative values.

% solution_end

% solution_start

Rubric: - 3 points in total

    1 point for describing and/or comparing the statistical features of the distributions in a reasonable way (e.g., commenting on similarities or differences in skewness, variability, etc.)
    0.5 points for each correct distribution
    0.5 points for each correct justification

% solution_end

**Question 2**

Fit and assess the goodness of fit of the selected parametric distribution functions to the dataset. Use (at least) Kolmogorov-Smirnov test and one graphical technique. For the graphical technique, choose between the QQplot and logscale plot. Describe in a few sentences how the chosen parametric distribution functions performs.

_Remember to use quantitative information based on the goodness of fit metrics that you have used. Also, you can include some examples of the differences in the computed and observed non-exceedance probabilities._

% solution_start

- Logscale plot: This technique allows to visually assess the fitting of the parametric distribution to the tail of the empirical distribution. For v, the lognormal distribution fits very well in the tail. The beta distribution for G also yields an acceptable fit, but deviates from the empirical distributions in the right tail. Specifically, it underpredicts the exceedance probability of high wind speeds, which may lead to an underestimation of the risk of high wind speeds.
- QQplot: Here, we can see that the fit of the parametric distribution to the empirical distribution is very good in both cases, with the only exception being the tails, as discussed in the logscale plot.
- Kolmogorov-Smirnov test: remember that the test statistic measures the difference between two distributions. The p-value then represents the probability of observing a difference at least that large for a sample from the assumed distribution. If p-value is lower than the significance ($\alpha = 0.05$, for instance), the null hypothesis is rejected. Considering here $\alpha = 0.05$, we cannot reject the hypothesis that v comes from a lognormal distribution, or that G comes from a beta distribution.

% solution_end

% solution_start

Rubric: - 3 points in total

    1 point for recognizing that both distributions have similar fits (0.5 points for a convincing explanation that deviates from that) in the graphical logscale or QQ plot
    0.5 points for the correct KS p-value for $v$ (0.579) or for the correct computation if they chose a different pdf 
    0.5 points for the correct KS p-value for $G$ (0.089) or for the correct computation if they chose a different pdf
    0.5 points for the correct interpretation of the KS p-value for $v$: cannot reject H_0
    0.5 points for the correct interpretation of the KS p-value for $G$: cannot reject H_0
    (also full points on the last two items if the interpreted wrong KS-values correctly)
 
% solution_end

**Question 3**

Propagate the uncertainty through the equation to estimate the wind gust factor, $F$, using both observations and simulated samples. Provide a bulleted list that summarizes differences between the two obtained distributions.

- your
- bulleted
- list
- here

Compare the simulated samples and observations $(v,G)$ in a scatter plot, then prepare a bulleted list that describes the differences. Is there anything you could improve in the analysis? Provide with recommendations to improve the performed analysis. They can be both about the univariate distributions and about the propagation of uncertainty method you have used.

_Include your figure here. Be sure to use high contrast data symbols/colors and a legend to differentiate the two data sets clearly._

% solution_start

- In the PDF plot, we can see significant differences in the observed and simulated distributions for $F$. The observed distribution is much narrower, and has wind gust factors that start at and go into the tens. By contrast, the simulated distribution for includes values below $1$, which should not be possible: the gust speed cannot be lower than the wind speed, so we should always have $F \leq 1$.
- Similarly, we can see in both the PDF and CDF plots that the simulated wind gust factors are dramatically larger than the observed ones. This includes unrealistically large factors, some even reaching beyond 100, which seems scarcely physically possible.
- As may be expected, the observations are focussed along a thin band, indicating strong positive correlation. By contrast, the simulations are spread much more broadly, freely combining wind and gust speeds of different velocities. This is a consequence of the assumption of independence in the simulations.
- **Some suggestions:** The fit got $v$ was already excellent, and also choosing a lognormal distribution for $G$ might yield better results (we limited ourselves to a beta distribution here for the sake of the exercise). Accounting for the dependence between the two variables is an absolute must. 

% solution_end

% solution_start

Rubric: - 3 points in total

    0.5 points for recognizing that the simulated distribution of $F$ is much broader than the observed distribution of $F$
    0.5 points for recognizing that the distribution includes unphysical values (F lower than 1, extremely high factors, etc.)
    1 point for recognizing that there is a relationship/dependency/correlation in the observations that the simulation does not capture
    1 point for making reasonable suggestions for improvements (capturing the dependency, truncating unphysical values, etc.)
    (half points for slight deviations or imperfect answers)
 
% solution_end


**Last Question: How did things go? (Optional)**

_Use this space to let us know if you ran into any challenges while working on this GA, and if you have any feedback to report._

> By Max Ramgraber, Patricia Mares Nasarre and Robert Lanzafame, Delft University of Technology. CC BY 4.0, more info [on the Credits page of Workbook](https://mude.citg.tudelft.nl/workbook-2025/credits.html).
