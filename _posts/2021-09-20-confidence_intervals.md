---
layout: post
title: Confidence intervals from hypothesis tests
date: 2021-09-20
author: Paul Boes
katex: true
---

Confidence intervals are a standard measure of confidence in data analysis: Almost any piece of software you use to run an OLS regression will provide you with a confidence interval - usually some range $$[a,b]\subseteq \mathbb{R}$$ for every estimated coefficient - as part of the summary of the regression. The question what this interval signifies is commonly answered by saying that, provided the assumptions of OLS regression hold, with high probability the true value of the quantity you estimate lies within the given interval.

This answer confused me when I first heard it. Clearly an interval either contains a value or it doesn't. So where does the probability come from? It turns out that the idea is simple (and quite independent of OLS regression) and that we can understand regression confidence intervals based on a simple but elegant connection between confidence intervals and hypothesis tests. But as is often the case, explanations online either lacked the kind of formal treatment that makes me actually understand something, or the math was too specifically focussed on OLS regression in order for me to understand how it depends on the latter's many assumptions. So here I want to briefly present this connection in a self-contained way.[^nothing_new]

Let me first introduce some notation: We have a family of random variables $$X_\theta$$ that all take values in some measurable space $$\mathcal{X}$$ and whose probability distributions $$P_\theta$$ are parametrized by elements $$\theta$$ of another measurable space $$\Theta$$. In the context of a regression we can think of every $$x \in \mathcal{X}$$ as data that I sampled, $$X_\theta$$ as the random variable describing the process of sampling, and $$\theta$$ as the (unknown) value of the coefficients in a linear model. We abstractly describe an estimator as a function $$f: \mathcal{X} \to \Theta$$ that maps any value of the random variable to some value $$\theta$$ (think mapping a sample to an estimate of the coefficients). 

A confidence interval then is a function that that maps values $$x$$ into sets of parameter values such that, with sufficiently high probability contains $$\theta$$, if $$x$$ was sampled from $$P_\theta$$. Lets formalize this. Given a confidence level $$\alpha \in [0,1]$$, call a function $$g: \mathcal{X} \to  \mathcal{P}(\Theta)$$ an *$$\alpha$$-confidence interval map* if it has the property that, for any $$\theta \in \Theta$$, 

$$ \mathrm{Prob}_{x \sim P_\theta}(\theta \in g(x)) \geq \alpha.$$ 

Here, $$\mathcal{P}(\Theta)$$ denotes the power set (set of subsets) of $$\Theta$$. The most fruitful way to think about confidence intervals (at least for me) is then that there is a *procedure* (represented by $$g$$) for generating confidence intervals from samples, such that, if I follow this procedure, then regardless of the value of $$\theta$$, intervals generated according to this procedure will contain $$\theta$$ with probability $$\alpha$$.[^confidence_interval]

But now that we have understood what confidence intervals are about, the natural question is how to construct them. Here, we can use a simple but nice connection to hypothesis tests: For a hypothesis test, I use a data sample and an estimator to decide whether I can reject a null hypothesis about the true value of an unknown parameter with some significance threshold. More precisely, a hypothesis test should accept a false null hypothesis with a probability at most  $$\alpha$$. Let's again formalise this idea: For a significance threshold $$\alpha \in [0,1]$$, call a function $$h: \Theta \to \mathcal{P}(\Theta)$$ an *$$\alpha$$-hypothesis test for estimator $$f$$* if, for any $$\theta$$, $$\mathrm{Prob}_{x \sim P_\theta}(f(x) \in h(\theta)) \geq 1-\alpha$$ and $$\theta \in h(\theta)$$. The way we turn this into a hypothesis test is via the procedure "If $$f(x) \notin h(\theta)$$, reject the null hypothesis that $$x$$ was sampled from $$P_\theta$$ with significance threshold $$\alpha$$."

Now, the nice thing is that we can construct an $$1- \alpha$$-confidence interval map from any estimator $$f$$ and $$\alpha$$-hypothesis test for $$f, h$$: Simply define 

$$g(x) := \{\theta \in\Theta \quad \mathrm{ s.t. } \quad f(x) \in h(\theta)\}.$$

This maps any sample $$x$$ to the set of parameter values $$\theta$$ for which the estimator $$f(x)$$ survives the hypothesis test defined by $$h$$ and the null hypothesis $$\theta$$. To see that this simple construction works note that, for any $$\theta$$,

$$\mathrm{Prob}_{x \sim P_\theta}(\theta \in g(x)) = \mathrm{Prob}_{x \sim P_\theta}(f(x) \in h(\theta)) \geq 1- \alpha$$,

where we used that $$\theta \in g(x) \Leftrightarrow f(x) \in h(\theta)$$.

To make all of this less abstract, let me translate the above into the common case of a simple linear regression model: Every $$x$$ is a data sample consisting of $$n$$ pairs $$(y_i, z_i)_{i=1}^n$$such that, for each pair we assume that it was generated according to the model $$Z_i = \beta Y_i + \beta_0 + \epsilon_i$$, with additional assumptions about how the various errors terms are distributed, etc. If we want to use an $$x$$ that we sample to generate a confidence interval (with confidence level $$95\%$$) for the coefficient $$\beta$$, this means we are usually given the formula[^change_alpha]

$$[\hat{\beta} - 1.96 \times SE(\hat{\beta}), \hat{\beta} + 1.96 \times SE(\hat{\beta})],$$

where $$\hat{\beta} \equiv \hat{\beta}(x)$$ is the OLS estimator of $$\beta$$ and $$SE(\hat{\beta}) $$ is its standard error. Using the above connection to hypothesis tests, we can identify this confidence interval map (since both OLS estimator is a function of the data, the above defines a map from data to sets of parameter values) as the one that is induced by an optimal[^why_optimal] $$5\%$$-hypothesis test for the normalised OLS estimator : That is, we set $$f(x) \equiv \hat{\beta}(x)/SE(\hat{\beta}(x))$$ 

$$h(\theta) = \arg \min_{[a,b] \subseteq \mathbb{R}: \mathrm{Prob}_{x \sim P_\theta}(\frac{\hat{\beta}}{SE(\hat{\beta})} \in [a,b]) \geq 0.95} b - a,$$

which is a somewhat convoluted way to write that we define $$h$$ as mapping any value $$\theta$$ to the smallest (in terms of the Lebesgue measure) interval such that, under the null hypothesis $$\theta$$,  the probability that the expression $$\hat{\beta}/SE(\hat{\beta})$$ is contained in this interval is at least $$95\%$$. Now, it conveniently turns out that under the usual assumptions of simple linear regression models, we know the distribution of this expression analytically to be a Student's t-distribution, which is a bell-shaped distribution, centered around $$\theta$$. Hence, $h$ defines a valid $$95\%$$-hypothesis test for $$\hat{\beta}$$  and we can analytically evaluate its value (which is also called $$t$$-value) as

$$h(\theta) = [\theta - 1.96, \theta + 1.96]$$.

Finally, in order to evaluate $$g$$ based on $$h$$, let's think about the set of values $$\theta$$ such that $$f(x) \in h(\theta)$$. Since changing $$\theta$$ simply shifts $$h(\theta)$$ by a corresponding amount, we see that these are all the values within the interval $$[f(x) - 1.96, f(x)  + 1.96$$]. But since this is now a confidence interval for the normalized OLS estimator, in order to get an interval for $$\hat{\beta}$$, we multiply this interval by the standard error, resulting in exactly the confidence interval we were given above.

___

[^nothing_new]: None of this is original, even the Wikipedia article on confidence intervals touches everything I say, but it also just states connections and doesn't show them. 
[^why_optimal]: A hypothesis test is called optimal if it always maps every hypothesis to the smallest set of candidates that are to survive the test, where size is measured by the measure on the space.
[^change_alpha]: Changing the value of $$\alpha$$ only changes the factor in front of the standard error
[^confidence_interval]: An equivalent way of putting this is that the confidence interval is a random variable (namely, the one induced by $$P_\theta$$ and $$g$$).

