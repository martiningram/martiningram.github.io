---
layout: page
title: About
permalink: /about/
---

<img src="/images/photo.png" alt="Me" width="150"/>

My name is Martin Ingram. I'm a PhD Student at the University of Melbourne,
Australia, supervised by [Nick
Golding](https://research.curtin.edu.au/researcher/nick-golding-fea4f81a/) and
[Damjan Vukcevic](http://damjan.vukcevic.net/). I completed my undergraduate degree in
Natural Sciences (Physical) at the Unversity of Cambridge in 2014 and a Master's
degree in Computing Science at Imperial College, supervised by [William
Knottenbelt](https://www.imperial.ac.uk/people/w.knottenbelt) in 2015. You can
find my full resume [here]({{ site.baseurl }}/misc/cv.pdf).

I'm interested applying Bayesian statistics to practical problems. You can view
my publications on [Google
scholar](https://scholar.google.com/citations?user=AZ-A7AEAAAAJ&hl=en).

My github account is here: [github](https://github.com/martiningram)

One current focus is on researching variational inference algorithms that are
both fast and accurate enough. I am doing some work on this using the JAX
package in python. Some code for this is in the [SVGP
repository](https://github.com/martiningram/svgp).


### Papers

**How to extend Elo: a Bayesian perspective** _Ingram_ (2021): Published in
[JQAS](https://www.degruyter.com/view/journals/jqas/ahead-of-print/article-10.1515-jqas-2020-0066/article-10.1515-jqas-2020-0066.xml). This
paper discusses how the Elo rating system, originally developed for chess but
now popular in many sports, can be related to Bayesian inference and (extended)
Kalman filtering. The connections are used to develop principled extensions of
Elo which are shown to outperform existing methods when used for prediction.

**Multi-output Gaussian processes for species distribution modelling** _Ingram,
Vukcevic, Golding_ (2020). Published in [Methods in Ecology and
Evolution](https://besjournals.onlinelibrary.wiley.com/doi/epdf/10.1111/2041-210X.13496). We
explain how multi-output Gaussian processes (MOGPs) can be used to model the
distribution of multiple species. We use variational inference to scale the
approach to large datasets and show that MOGPs outperform other approaches,
especially for species that are rarely observed.

 **Space-Time VON CRAMM: Evaluating Decision-Making in Tennis with Variational
generatiON of Complete Resolution Arcs via Mixture Modeling** _Kovalchik,
Ingram, Weeratunga, Goncu_ (2020): Available on
[arXiv](https://arxiv.org/abs/2005.12853). We use an infinite Bayesian Gaussian
mixture model to model player and ball trajectories in tennis and use it to
develop a number of metrics, including an expected shot value, to evaluate
players' decision making.

**A point-based Bayesian hierarchical model to predict the outcome of tennis
matches** _Ingram_ (2019): Published in
[JQAS](https://www.degruyter.com/view/journals/jqas/15/4/article-p313.xml). I
present a Bayesian hierarchical model to predict tennis matches, incoporating
surface and tournament effects into a dynamic Bradley Terry model that is fit
using Stan. [PDF]({{ site.baseurl }}/papers/bayes_point_based.pdf).

**Estimating the duration of professional tennis matches for varying formats**
_Kovalchik, Ingram_ (2018): Published in
[JQAS](https://www.degruyter.com/view/journals/jqas/14/1/article-p13.xml).

**Adjusting bookmaker's odds to allow for overround** _Clarke, Kovalchik,
Ingram_ (2017): Published in the [American Journal of Sports
Science](http://www.sciencepublishinggroup.com/journal/paperinfo?journalid=155&doi=10.11648/j.ajss.20170506.12)

**Hot heads, cool heads, and tacticians: Measuring the mental game in tennis**
_Kovalchik, Ingram_ (2016): Presented as a poster at the 2016 MIT Sloan Sports
Analytics Conference. [PDF]({{ site.baseurl }}/papers/hot-heads-cool-heads.pdf).

### Contact me

[martin.ingram@gmail.com](mailto:martin.ingram@gmail.com)
