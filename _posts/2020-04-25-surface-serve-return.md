---
layout: post
title: ATP Serve & Return skills by surface since 1991
---

{% include image.html url="/images/sampras_nadal.jpg" description="<i>Rafael Nadal at the French Open, Pete Sampras at Wimbledon. Photograph: Mike Hewitt/Getty Images (Sampras), AP: Michel Euler (Nadal)</i>" %}

A few weeks ago, I wrote about how tennis players can be analysed with [a model that estimates their serve and return skill](https://martiningram.github.io/historical-serve-return/) for ATP players since 1991. That model assumed an overall average skill for each player on serve and return that's constant across surfaces. That's a good first look,  but as tennis fans, we know that surfaces play a huge role in the sport. Just look at some of the top players: Rafael Nadal, while impressive on all surfaces, is particularly lethal on clay, winning 12 of his 19 Grand Slam titles at the French Open. Pete Sampras won seven of his 14 slam titles at Wimbledon, but never got past the semi-finals in Paris. Clearly, there are big skill differences here.

To analyse how much surface effects influence players' serve and return skills, I decided to fit another model. This new model is similar to the old serve and return model, except that I now also allow both skills to vary by surface. To do that, I use hard courts as the reference court, and estimate how much better each player does on grass and clay, both on serve and return. Note that this misses one surface: carpet was popular throughout the 90s, but very few matches have been played since 2010. I therefore discarded carpet matches for this initial look, though it might be fun to investigate this forgotten surface in more detail at some point in the future.

#### Surface specialists

The first thing we can look at is how much different players improve on the different surfaces. To take a look at that, I summed the improvements on serve and return for clay and grass compared to hard, and plot the two against each other:

![surface_specialists]({{ site.baseurl }}/images/surface_specialists_atp.png)

One way to think about this plot is to divide it into four quadrants, which I've annotated in the corners. What do the numbers here mean? To win a tennis match, both your serve and return skill are crucial. Doing better on serve means you're harder to break, and doing better on return means you have a greater chance of breaking your opponent. A player may do better at serving on grass than on hard, but if their return suffers more than their serve improves, they are expected to do worse overall. The sum thus represents a kind of net improvement, taking into account both serve and return.

The top left quadrant contains players who play better on grass than on hard courts, but worse on clay. The standout player here is Pete Sampras, who gets one of the largest boosts to his serve & return skill on grass (over 2.5%), but also takes the largest hit on clay (-0.05). The quadrant is filled with grass court legends, including Becker and Edberg, who all excelled on this surface.

The bottom right quadrant contains the clay courters. These players are better on clay than on hard courts, but worse on grass. Guillermo Coria and Dominic Thiem stand out here. Nadal is an interesting case: he gets a huge boost on clay as you would expect, but he does not take as big a hit on grass as, for example, Coria. That's perhaps not surprising given that Nadal has won two Wimbledon titles, even though he has had some early losses there too.

The other two quadrants are perhaps a little less expected. The bottom left one contains players who are estimated to have played best on hard courts. It's a little surprising then to find three French Open winners -- Agassi, Chang and Lendl -- in this quadrant. Agassi makes sense, I think: he won six of his eight slams on hard. Lendl is a really intriguing case. Though a force at the French throughout the 80s, he skipped it in 1990 and 1991 to prepare for Wimbledon and lost in the second in 1992, followed by two first round losses in 1993 and 1994. It seems like his heart wasn't really in it anymore. Chang is perhaps the hardest to explain, given that he did reach the final of the French in 1995, but the model suggests he was most effective on hard courts.

Finally, the players in the top right corner are estimated to prefer both clay and grass courts over hard courts. The effects are relatively small compared to the clay and grass specialists, and Gasquet and Kohlschreiber seem to be the players most squarely in this camp.

#### Serve & return plots by surface

How do these preferences shift the serve and return plots? To keep the post short, I'll post the plots and then point out some general things I took away from them:

![hard skills]({{ site.baseurl }}/images/serve_return_skills_hard_atp.png)
![clay skills]({{ site.baseurl }}/images/serve_return_skills_clay_atp.png)
![grass skills]({{ site.baseurl }}/images/serve_return_skills_grass_atp.png)

Some things I took away:

* Sampras really shifts on grass compared to the other surfaces. If he were playing today, he would be a serious contender to win Wimbledon, with his overall summed skill slightly behind Federer and Djokovic and roughly on par with Murray. He doesn't even make the top 50 on clay however -- he really didn't seem to like that surface!
* By contrast, Nadal is a beast on clay, as you'd expect. His skill is particularly noticeable on return, where he outperforms everyone else by a mile.
* The 1990s players seem to be most prominently represented on the grass courts. In addition to Sampras, Edberg is estimated to be quite strong, especially on return, despite the 90s being the tail end of his career, and the top 50 contain quite a few players who peaked in the 1990s. They seem to be least well represented on clay, and I wonder if some of this is due to the changes in stringing technology.
* The big four stand out on all surfaces, as you might expect. Nadal has a clear edge on the other three on clay, and Murray is most competitive on grass. Federer and Djokovic are pretty close on the surfaces, with Djokovic having a slight edge on clay and on hard, but Federer perhaps having a slight advantage on grass overall. Nadal is slightly behind them on both hard and grass.

As I mentioned already, it's always important to take things with a grain of salt. For one, comparing the 1990s with the 2010s might not be fair due to advancements in technology. For another, these skills are career averages, and peak ratings might tell a different story -- for example, Djokovic at his peak on clay might trouble Nadal. Still, I hope you enjoyed this deeper dive into surface skills!
