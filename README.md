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
Main steps:
- choose the "subject" of your test — **unit of diversion**
- choose the "population" — which subjects are eligible (e.g. everyone?, only from a particular region?, only on iOS?, etc. )
- choose the size of each group — properly size your experiment
- define the duration of running the experiment

Unit of diversion:
- user id
    - stable and unchanging
    - personally identifiable
- cookie
    - changes when you switch a device or a browser
    - user can clear cookies
- event
    - non consistent experience
    - use only for non-user-visible changes
- device id (less common):
    - only available for mobile
    - tied to a specific device
    - personally identifiable
    - doesn’t have cross-platform consistency that a user id can have
- ip address (less common):
    - changes when user’s location is changed
    - not recommended in general

What to keep in mind when choosing how to divert traffic is:
- user consistency, e.g. when we are using user id, a user has a consistent experience even if they are changing devices as long as they are signed in
- ethical considerations, e.g. if you are using a user id that means that a user is identifiable and you have to worry about all the issues described in the lesson 2 and also you have to deal with a user consent
- variability

Empirically computed variability is usually much higher than analytical computed variability. That’s happening when the unit of analysis is different than a unit of diversion. 

**Unit of analysis** — whatever your denominator is. 
But if your unit of diversion is a cookie or a user id your variability can be higher. 

When you computing variability analytically you are making an assumption not only on the distribution of the data but also you are making an assumption on what is considered to be independent. When you are doing cookies or user ids based diversion that independent based assumption is no longer valid because the groups of events will be correlated together and that actually increases the total variability. 

When *unit of analysis = unit of diversion*, variable tends to be lower and closer to analytical estimate. 

For user visible changes you definitely use a cookie or a user id as a unit of diversion. 

The variability of all data as measured by the pooled standard error usually is lower than for the filtered data. Mostly because there is so much more data when you use all of it, without filtering for only one particular strata. This will often be the case in practice. Also in practice, your data will actually be a mix of different populations almost every time. And when you filter you are going to get a smaller but also more uniform population. Which means that for the same number of data points the variability of the filtered data is likely to be lower. 

When to use cohort instead of a population for your experiments:
- looking for learning effects
- examining user retention
- want to increase user activity
- anything requiring user to be established 
But keep in mind that when using cohorts control should be a comparable cohort. And that cohorts limit your experiment to a subset of the population and that can affect variability. 

We’ve already discussed earlier how to size an experiment based on: 
- your practical significance
- your statistical significance
- sensitivity you want. 

All those things can affect the variability of your metric:
- choice of metric
- choice of the unit of diversion
- choice of population 

An example: if our metric is click-through rate and our unit of diversion is cookie, but it turns out we need too many page views. We can apply following strategies to reduce the number of page views needed:
- increase practical significance boundary, alpha or beta
- change the unit of diversion to page view
- target experiment to specific traffic
- change metric to cookie based click-through-probability

When you know the size of your experiment you have to decide:
- the duration of the experiment
- when to run it (is to run it during holidays a good idea or not)
- what fraction of your traffic you are going to send through the experiment

**Learning effects** — when you want to measure user learning (whether a user is adapting for a change or not).   
For example:
- change aversion — when a user don’t like anything new
- novelty effect — an opposite thing, when something new attracts a user a lot for a short period of time 
But in both cases over time a user will plateau to a different behaviour. 

To deal with learning effect keep in mind the following:
- choosing the unit of diversion correctly - you need a stateful unit of diversion like a cookie or a user id
- you probably want to be using a cohort as opposed to just a population. you choose cohort based on how long users were exposed to a change or how many times they’ve seen it
- risk and duration - you don’t want to put users through a long exposer, because, maybe you want to test another changes as well (so you, probably it would be better to run your experiment through a longer period of time but on a smaller group of users). 
- use both pre-periods (A/A tests) and post-periods (another A/A test) of the test to study users behaviour and their learning effects 

The very important thing is to go through your work of designing an experiment properly. 

Keep in mind that variability of your Metric can really change depending on what you choose as your unit of diversion. 

A/B testing is always an iterative process. 

Keep an eye on your data especially during the very first days of you running the experiment to be able to detect immediately whether something went wrong or not. 
  
A python code snippet how to calculate A/B testing groups size: [go to the snippet](https://gist.github.com/nktnlx/963e5b194ea1fb895bf362c6dd8a444c). 

The way to build A/B testing intuition is to gain a lots of practice. 


## 5. Analysing Results  
Plan for the lesson:
- sanity checks
- single metric
- multiple metrics
- analysis gotchas

Sanity checks are done before starting analysing experiment results to be sure that your experiment was done properly:
- check size of the control and treatment groups
- check that invariants (metrics that are not supposed to be changed) are not changed

If one of your sanity checks fail — do not proceed. Go and discover why it actually failed. 
Have a look at the pre-test period. Do you see the same inconsistency in data? If  yes - something could be wrong with your infrastructure in general, if not - it has something to do with your experiment.   
The most common mistake here is data capture. Especially if you are checking a new feature. And another reason could be the experiment setup. 
If it is just a learning effect of your users you won’t see a huge increase in the beginning it will grow steadily over time. 

If your results aren’t significant, but you were expecting they would be. Instead of running for longer to get more users when you don’t like the results, you should be sizing your experiment in advance to ensure that you will have enough power the first time you look at your experiment. See [this post](https://www.evanmiller.org/how-not-to-run-an-ab-test.html) for more details.  

If you write A/B testing software: Don’t report significance levels until an experiment is over, and stop using significance levels to decide whether an experiment should stop or continue. Instead of reporting significance of ongoing experiments, report how large of an effect can be detected given the current sample size.  

If our results are not statistically significant:
- take a much longer look at your results
- break it down to different platforms, different days of the week, different stratas of users, etc. 
- it may help you find bugs in experiment setup
- as well as it might help you to come up with new hypothesis about how people are reacting to the experiment
- cross check your results with another methods (e.g. parametric VS non-parametric)

With click-through probability we are dealing with binomial distribution, while when our metric is a click-through rate we more likely to have a poisson distribution (so it’ll be a good idea to estimate the variance empirically).

[Sign calculator](https://www.graphpad.com/quickcalcs/binomial1.cfm)
How to do a sign test: you look at your metric day by day. Define how many times the test results are better than in control group, for example 8 of 14 days the test was better than control. Then calculate the p-value with the probability of 0.5 (complete random results) and look at it. If it is less than 0.05 then the sign test is statistically significant.  
Sign test has a lower power than an effect size test which is frequently the case for a non-parametric test, that is a price for not making data distribution assumptions. 

Simpson’s Paradox example: women has higher acceptance rate for each department, but overall an acceptance rate for women is lower than for a man. 

**Multiple comparisons** — the more things you test, the more likely you are to see significant differences just by chance.   
Example: *"Suppose the treatment is a new way of teaching writing to students, and the control is the standard way of teaching writing. Students in the two groups can be compared in terms of grammar, spelling, organisation, content, and so on. As more attributes are compared, it becomes increasingly likely that the treatment and control groups will appear to differ on at least one attribute due to random sampling error alone."* For comparing simultaneously three metrics at a confidence level of 95% the probability to have at least one false positive is: *1 - 0.95\*\*3 = 0.143* or 14.3%

Bonferroni correction:
- simple to calculate
- no assumptions (on independence of metrics)
- conservative (guarantees to give alpha_overall at least as small as specified)

A more robust method to use for multiple comparison correction is False Discovery Rate (FDR). [Wiki page on FDR](https://en.wikipedia.org/wiki/False_discovery_rate).  

Not to deal with multiple comparisons people might want to use only one metric — OEC (Overall Evaluation Criteria). Best OECs have a good balance between long-term investment metrics and short-term ones. Because you don’t want to loose one in pursuing another. To come up with the best one you have to do a lot of business analysis of your company. For an example our company want to have 25% increase in revenue and 75% increase in site visits. Those will be weights for your compound OEC. 

When you have a statistically significant result of your test you have to decide:
- do you understand the change 
- do you have to launch or not to launch

If you have misguided results (some metrics are significant and some are don’t):
- do you understand the change
- you have to have an intuition on many other experiments and their results to make a final decision

For small changes to have a change in only one metric can be completely okay. And if for a big change we see a change in only one metric it can be a sign that something somewhere went wrong. 

To launch or not:
- do I have statistically significant and practically significant results in order to justify the change
- do I understand what that change has actually done with regards to user experience 
- is it worth it to launch the change

What will be remembered at the end of the day: did you recommend to launch it or not and was it the right recommendation. 

It’s always a good idea to ramp up any change (to launch it step by step on fractions of users).  
But keep in mind that an effect can actually flatten out if you gradually ramp up the change. 

Seasonal factors: when students go on a vacation the behaviour of internet changes and then it comes back to normal again.  
Shopping behaviour changes a lot before holidays and Black Fridays. 

Cohort analysis can help to track how users adopt to a change and how their behaviour changes over time. 

Lessons learned:
- check, double check and triple check that your experiment was setup properly 
- you are not only for statistical significance, you are making business decisions
- don’t forget about business costs to implement the change (backend, support, customer service, opportunity cost, etc.)

THE END
