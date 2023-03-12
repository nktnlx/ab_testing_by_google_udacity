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
Main Principles:
- risk - what risk is the participant of the survey being exposed to (the risk should be less than a minimal risk. Experiments that about medical or financial conditions could lead to risks that are above minimal risk level). 
- benefits - what benefits might be the outcome of the study. Benefits are around improving a product. It is important to be able to state what the benefit would be from completing the study. 
- alternatives - what other choice do participants have. In online experiments, the issues to consider are what the other alternative services that a user might have, and what the switching costs might be, in terms of time, money, information, etc.
- data sensitivity - what expectation of privacy and confidentiality do participants have:
    - Do participants understand what data is being collected about them?
        - does it include financial or health data
        - is it personally identifiable
        - what is security protocol and level of confidentiality
    - What harm would befall them should that data be made public?
    - Would they expect that data to be considered private and confidential?

If the study is on existing public data, then there is no expectations of further confidentiality. 

**Identified data** means that data is stored and collected with personally identifiable information (name, phone number, passport number, etc).  
**Anonymous data** means that data is stored and collected without any personally identifiable information.
Data can be considered pseudonymous if it is stored with a randomly generated id such as a cookie that gets assigned on some event, such as the first time that a user goes to an app or website and does not have such an id stored.  
**Anonymised data** is identified or anonymous data that has been looked at and guaranteed in some way that the re-identification risk is low to non-existent, i.e., that given the data, it would be hard to impossible for someone to be able to figure out which individual this data refers to.

When you collect users data:
- are users being informed?
- what user identifiers are tied to the data?
- what type of data is being collected?
- what is the level of confidentiality and security? who in your company will have an access to this data?

If you teach someone A/B testing you should provide such information to them:
- which questions to consider when evaluating ethics of your experiments
- data policy detailing acceptable data uses
- principles to uphold while running experiments


## 3. Choosing and Characterising Metrics   
The first thing we have to do is to define a metric(s), in other words how we are going to measure success of our experiment. 
The should be two kind of metrics:
- invariant — shouldn’t change across our treatment and control groups — those are sanity checks that you experiment was designed properly and is running with our serious bugs
- evaluation metrics:
    - high-level business metrics:
        - how many users you have,
        - how many money you make
        - what is your market share is
        - etc. 
    - detailed metrics:
        - about user experience, e.g. how long they stay on the page, etc. 
        - active users
        - click-through rate probability
        - etc.

If you work towards improving one metrics that’s fine. But imagine if different teams in your company are working towards different metrics. If you are in that kind of a situation, you can create a composite metric, a.k.a Overall Evaluation Criteria (OEC). 

Also you have to consider is how applicable metric is when design an experiment. Ideally you should have one or two metrics that you can use across the entire suite of experiments you perform in your company.  It’s much better to use a metric that’s less optimal for your test, if you can use it across the suites that can do the comparison, that it is to come up with the perfect metric for your test. Whenever you do something custom, it just introduces more risk. 

When coming up with the high-level concepts for metrics, first of all you have to keep in mind what is your business objective and also that your business has to be financially sustainable (it has to make money). 
You can use a customer funnel for that process:
- homepage visits
- course list visits
- visits to course pages
- accounts created
- enrolments
- coaching use
- completion
- job offers got
Each stage in the funnel is a metric here (number of users)! And you can also convert it to a rate by dividing the number of users on one stage by the number of users on an another stage.  And you can transform rates into rates of probabilities. 

Difficult metrics are when:
- you don’t have access to the data (e.g. an average happiness of shoppers or probability of finding information using search)
- it takes too long to collect the data (e.g. rate of returning for the second course among students who have finished the first course)

Other techniques to use for metrics that are hard to collect in a short period of time:
- surveys on customers preferences and lifestyle:
    - multiple-choice questions
    - free form responses
    - a combination of both
- retrospective analysis (is really best for establishing a correlation and not a causation)
- focus groups
- user experience research (UER) — a combination of observing users doing tasks and asking them questions:
    - in lab
    - field studies
    - user’s diary studies (users are asked to self-document their behaviour) — but you can encounter issues with self-reporting bias
- long-term prospective experiments (including long running A/B tests)
- human evaluation (crowed sourcing) — people are paid to complete a specific task. Can be very helpful for getting a lot of labeled data. 
- you can use all of these techniques in conjunctions one to another 

When choosing a technique that’s fits you best you have to have in mind:
- do you want to figure out how to measure a particular user experience?
- or do you want to validate a metric?
    - external analysis
    - retrospective analysis are best for it. 

The bigger the decision you are about to make, the more time you may want to invest in getting additional data. 

[Additional techniques pdf link](https://s3-us-west-2.amazonaws.com/gae-supplemental-media/additional-techniquespdf/additional_techniques.pdf). 

Metrics for experiments:
- define
- build intuition — you have to know what changes are should be expected and what shouldn’t be expected from your experiment
- characterise

Different ways to calculate a metric for clicks:
- rate — number of clicks divided by number of page views
- cookie probability — for each defined time interval, number of cookies that click divided by number of cookies visited
- page view probability — number of page views with a click within defined time interval divided by number of page views. 

We don’t want to use data in our experiment coming from:
- spam
- bots
- competitors random clicks (malware that tries to mess your experiments and metrics)
So we have to de-bias our data (filter it carefully). Usually extremely long and active sessions are filtered out. 

Sometimes looking at data week over week or day over day, or slicing down to an individual user group is a great way to identify spam or fraud. 

Important characteristics of your metric:
- sensitively — picks up changes you care about
- robustness — metric is robust against changes that you don’t care about
- distribution

If you have a distribution that is lopsided with a very long tail, choosing the mean probably doesn’t work for you very well - and in the case of something like the Pareto, the mean may be infinite. That’s why it is important to know what distribution of data you actually have. 

Categories of summary metrics:
- sums and counts (e.g. number of users who visited page)
- means, medians, percentiles (e.g. mean age of users who completed a course)
- probabilities and rates:
    - probability has 0 or 1 outcome in each case
    - rate has 0 or more outcomes
- ratios — it is two numbers divided by each other, so it can have any value (e.g. Probability of a revenue generating click divided by Probability of any click)

If you use mean as your metric, you should keep in mind that means are very sensitive to outliers (mean is not that robust). Median is robust, but in some situations can’t change at all, so sometimes you have to think of using another statistic such as 90th or 99th percentile.  
A/A test is a good way to check robustness of a metric. For example, if you see a lot of variability in a metric in an A versus A test, it’s probably too sensitive to be useful in evaluating a real experiment. 
Also A/A test is good for:
- testing is your randomisation function truly random
- do you have any issues with regards to bias
- do you have any weird population effects
- compare results to what you expect (sanity checks)
- estimate variance empirically and calculate confidence
- directly estimate confidence interval from A/A test

Or you can plot different statistics of a metric for various users and see whether it moves from user to user of not. If it starts to move it means that this metric is too sensitive or in other words not robust enough (like 90th and 99th percentile here on the picture below). 

If you use relative difference instead of absolute difference for your experiments you can stick with one practical significance boundary as opposed to having to change it as your system changes. 

To calculate a confidence interval you need:
- to know variance (or standard deviation)
- and to know the distribution 

Binomial distribution approaches a normal distribution when it gets larger. 

**Non-parametric methods** — using them you have a way to analyse data without making an assumption about what the data distribution is. These group of metrics can be noisier and computationally intensive, but they can also be very useful. 

If you want to launch any positive change in your experiment, then you can figure out whether there was one using a sign test (details on it will be later). 

When you have computed variance empirically from the sample data you have two choices:
- if you summary statistic distribution nice and normal you can use a normal confidence interval technique 
- if your data is more complex than that or you want to be really robust you can compute a non-parametric confidence interval. 

Standard deviation is proportional to the square root of the number of samples. 

If your bootstrap results is agreeing with your analytical estimate you are good to move on and have nothing to worry about. And if it is not, you should consider running a lot of A/A tests and really dig into data understanding what is going on. 

For empirical approach instead of SE we take a Standard deviation. 

Calculating variability empirically:
- we can take 20 A/A tests
- calculate the difference between groups for each of them
- take all the differences and sort them in ascending order
- eliminate the very first value from the sorted list and the very last value of the sorted list
- thus we’ll remain only with 90% of our data —> this will be for 90% empirical confidence interval, e.g. \[-0.01; 0.06\]
- then take the margin values of the confidence interval, sum them, e.g. -0.01+0.06=0.059
- then multiply what you get by the z-score, e.g. 0.059*1.65=0.097
- and now you have an empirical standard deviation 0.097
- if the difference is 0, than your confidence interval is \[-0.097, +0.097\]
Instead of running 20 A/A tests you can do the same with values obtained from bootstrapping. 

Variability for a metric can by so huge, that’s actually it’s not practical to use this metrics for your experiment even if the metric makes a lot of business or product sense. 

Being able to standardise the definition (how you are going to calculate it in particular) of a metric you are going to use is very important towards starting the A/B testing in your company at a whole different level. 

If you are not able make to move the mean statistic of your metric, try to look towards a higher percentile metric (85, 90, 95, etc. percentile) that you actually can get to move when you know that you’ve done something that is positive for the experiment. 

One more thing you have to think about when coming up with your metrics is does you metric have a big weekly variability. If your metric has a huge weekly variability, 28 days might make way more sense than 30 days for running the experiment. 

When you start doing A/B tests you are not able to predict everything about your data, so the key thing is that you are building intuition when trying to do them. You have to understand your data and you system. And it takes time and actual practice to get there. 

It’s good to start with analytical approach to estimate variability of your data (if you can actually do it) and then do it empirically.   

User behaviour can change over time, meaning that using metrics being a good idea in the past might not actually be a good metric for the feature. So you should always revise your system of metrics and experiments approach. 





## 4. Designing an Experiment
## 5. Analysing Results

