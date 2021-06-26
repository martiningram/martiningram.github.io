---
layout: post
title: Tennis rally lengths and the geometric distribution
---

{% include mathjax.html %}

Something I've always been curious about is how well the geometric distribution approximates rally lengths in tennis, so here's a quick blog post about it.

The [geometric distribution](https://en.wikipedia.org/wiki/Geometric_distribution) counts the number of Bernoulli trials to get one success. A simple example is tossing a coin: if we toss it until it comes up heads, the number of times we need to toss it before this happens will be distributed as
$$
\text{Geometric}(p),
$$
where $p = 0.5$ if the coin is fair.

What does this have to do with rally lengths? The connection is this: every time a player hits a ball in a rally, there's a chance that it's the last shot that's hit. It could be a winner or an error, ending the point either way. If we assume that the probability of hitting a point-ending shot is constant every time a player hits the ball, then we have exactly the same situation as with the coin.

How well does this hold up in practice? Here's some data from Wimbledon 2016-2019, obtained from [Jeff Sackmann's GitHub](https://github.com/JeffSackmann/tennis_slam_pointbypoint):

![Geometric Wimbledon]({{ site.baseurl }}/images/geometric_rally_length.png)

The orange bars are the observed rally lengths, where a rally length of 1 includes, as far as I can tell, aces and unreturned serves. I have also included double faults, and I've cut off rallies longer than 15 shots from this plot as they are very rare. I want to point out that I haven't worked with this dataset much and while I did some cleaning, there's a chance I may have missed some issues, so please take this analysis with a bit of a grain of salt.

Data aside, the blue bars are a geometric distribution with $p = 0.356$, which I found by computing the sample mean (see the expression for $\hat{p}$ [here](https://en.wikipedia.org/wiki/Geometric_distribution#Parameter_estimation) if you're interested). The fit is OK, but rallies of length 3 are considerably more likely than expected under the geometric, and rallies of length 4 are considerably less likely. I believe this is because the server often gets an easy return (shot 2) and can finish the point on the third shot, making it more likely to be the point-ending shot.

We can get a better fit if we're willing to group the number of shots together:

![Geometric Wimbledon Grouped]({{ site.baseurl }}/images/geometric_rally_length_grouped_wimb.png)

In this grouped version, the higher probability of 3 shots averages out with the lower one of 4 shots, and the fit is somewhat better. I got this plot by computing
$$
k' = (k - 1)// 2 + 1,
$$
where $k$ was the original rally length, and $//$ denotes integer division. The first bar, for example, represents $k' = 1$, the second $k' = 2$, and so on. Here, $\hat{p} = 0.577$.

What does all of this buy us? Well, if we're happy to conclude that rally lengths are approximately geometric, that sheds some light on things that are otherwise surprising. In particular, people are often surprised to hear that the majority of rallies end in under three shots. In fact, the second plot shows that about 60% of rallies are expected to end in under three shots at Wimbledon. What's more, the probabilities decrease monotonically: 1-2 shots is most likely, then 3-4, and so on. Of course, we could have inferred this from looking just at the data, but I think the geometric idea of repeated trials until a miss gives a nice intuitive explanation for why this is the case.

Finally, I thought I'd take a quick look at how things differ by slam:

![Geometric USO Grouped]({{ site.baseurl }}/images/geometric_rally_length_grouped_uso.png)
![Geometric French Grouped]({{ site.baseurl }}/images/geometric_rally_length_grouped_french.png)
![Geometric AO Grouped]({{ site.baseurl }}/images/geometric_rally_length_grouped_ao.png)

The legend lists the different $\hat{p}$ estimates for the grouped geometric. At $\hat{p}=0.496$, rallies are expected to be over most quickly at the AO, followed by $\hat{p} = 0.473$ at the US Open, and finally $\hat{p} = 0.381$ at the French. All three have longer rallies than Wimbledon, which had $\hat{p} = 0.577$. I found it pretty interesting that even when grouping shots, it seems that at the French, rally lengths of 3-4 shots are more likely than the geometric would predict. It looks like the serve+1 strategy might play a particularly big role there.
