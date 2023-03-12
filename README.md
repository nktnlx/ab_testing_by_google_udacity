# A/B Testing by Google
My notes on Online Experiment Design and Analysis Course by Google. The course covers how to choose and characterize metrics to evaluate your experiments, how to design an experiment with enough statistical power, how to analyze the results and draw valid conclusions.  

The course link on [Udacity](https://www.udacity.com/course/ab-testing--ud257?autoenroll=true)  

## Table of contents
1. [Overview of A/B Testing](#1-overview-of-ab-testing)
2. [Policy and Ethics for Experiments](#2-policy-and-ethics-for-experiments)
3. [Choosing and Characterising Metrics](#3-choosing-and-characterising-metrics)
4. [Designing an Experiment](#4-designing-an-experiment)
5. [Analysing Results](#5-analysing-results)  

## 1. Overview of AB Testing  
Amazon showed a 1% sales decrease for an additional 100 ms load time, and that a specific experiments at Google, which increased the time to display search results by 500 ms reduced revenues by 20% [[link]](https://www.exp-platform.com/Documents/GuideControlledExperiments.pdf).  

A/B testing process has been highly successful in helping LinkedIn make great product decisions based on real data from their users.

A/B tests, whether they fail or succeed, generate insights that can bring a quick return on investment and promote innovation.

Three questions to answer before deciding to A/B test something:
- could there be an actual impact to the company
- what will be the development effort to do the A/B test and to implement and maintain the new feature
- is this experiment going to teach us something fundamentally new

Kayak A/B test on SSL/TLS encrypted payment experiment [[link]](https://apptimize.com/blog/2014/03/kayaks-most-interesting-ab-test/). 

A good A/B testing solution should make it easy to explore all of the A/B tests that are going on in your organisation and how they are progressing. With our new system, every experiment needs to have a title, an owner, a description, and (when it’s finished) a conclusion. We were originally worried that people wouldn’t take the time to fill out descriptions, but in practice, they’re often several paragraphs and explain the motivation behind the experiment, the hypothesis, and any links or images that help in explaining the change.  
A good A/B testing solution should make it easy to explore all of the A/B tests that are going on in your organisation and how they are progressing [[link]](https://apptimize.com/blog/2014/07/how-khan-academy-uses-ab-testing-to-improve-student-learning/). 

Analyse data and logs that comes together with your A/B test. Thus you can get more insights and come up with new hypothesis to test later. 

Other techniques that can come together with A/B testing or sometimes substitute them:
- user experience research
- focus groups and surveys
- human evaluation
A/B testing gives you broad quantitative date and alternative techniques gives you very deep and qualitative data that are really complimentary to A/B testing. 

A/B testing originally comes from agriculture. Then there were clinical trials in pharmacy. 

The goal of any A/B test is to design an experiment that will be robust and give you repeatable results, so you can actually make a good decision about launching a new feature. 

A/B testing is everywhere right now. From FAANG to small companies. 

A/B testing steps:
- formulate testing hypothesis, e.g. *"Changing the button color from orange to pink will increase how many users will click on it."*
- choose a metric:
    - total number courses completed — is a bad metric, cause it is too slow
    - number of clicks — is a bad metric, cause there can be different amount of page views in each groups
    - number of clicks / number of page views (click-through rate - CTR) — a good one, but can work incorrectly if some of users will click the button multiple times
    - unique visitors who click / unique visitors to page (click-through probability - CTP) — the best metric for testing the given hypothesis
- review statistics
    - which distribution?
    - binomial distribution is good for situation when you have successes (clicks) and failures (no clicks). The binomial and normal distribution when approximated will have the same mean (mean=p) and *std = sqrt(p(1-p)/n)*
    - to use binomial distribution the events should be independent and probability (p) should be the same for all events
- design
    - size VS power trade-off (the smaller effect you want to detect or the more power you want to have the larger sample size you should have)
- analyse

In general you use CTR when you want to test the usability of your web site and you use CTP when you want to measure the total impact. 

Z score table chart [[link]](https://www2.math.upenn.edu/~chhays/zscoretable.pdf).  
[[How to read z-score tables]](https://www.had2know.org/academics/normal-distribution-table-z-scores.html). 

Z-score tables are based on a normal distribution that has a mean of 0 and a standard deviation of 1. If you have a set of normally distributed data with a different mean and standard distribution, you can transform it into standard form with the scaling equation (X-μ)/σ = Z.   


If *n \* p > 5* then you can approximate your binomial distribution with a normal distribution. 

Two-tailed vs. one-tailed tests:
- two-tailed allows to distinguish between:
    - a statistically significant positive result
    - a statistically significant negative result
    - no statistically significant result
- one-tailed allows to distinguish between:
    - a statistically significant positive result
    - no statistically significant result

If you're going to launch the experiment for a statistically significant positive change, and otherwise not, then you don't need to distinguish between a negative result and no result, so a one-tailed test is good enough. If you want to learn the direction of the difference, then a two-tailed test is necessary.

To establish that our results are statistically significant using hypothesis testing we need to calculate how likely it is that your results are due to change. 

**The Null hypothesis**:
- p_control = p_test
- p_test - p_control = 0

**The Alternative hypothesis**:
- p_test - p_control != 0

We want to reject Null hypothesis and conclude that our treatment had effect if the probability to obtain the difference we see by pure change is small enough (less than significance level alpha = 0.05/0.03/0.01). 

**Practical (substantive) significance** — what change is significant for us from a business perspective (what size of change matters to us).  

Statistical significance is about repeatability. When you setup an experiment you want to be sure that you have the guarantee that the results you’ll get are repeatable. 

You results have to be both statistically and practically significant. Statistical significance bar should be lower than the practical significance bar. 

*alpha = P(reject null | null is true)*    
*beta = P(fail to reject null | null is false)*   
*power/sensitivity = 1 - beta* (people usually choose to be 80%)  

[Sample size calculator](https://www.evanmiller.org/ab-testing/sample-size.html)

The closer your probability in control group comes to 0.5 the bigger SE you’ll get, thus the more page views you have to have in each group to run a successful experiment.  

When the results of test are uncertain (and you have to run an additional test with better power, but you don’t have time to do it) you have to communicate it to decision makers that they can probably take a risk to launch the feature based on the other data they have. 









## 2. Policy and Ethics for Experiments
## 3. Choosing and Characterising Metrics
## 4. Designing an Experiment
## 5. Analysing Results

