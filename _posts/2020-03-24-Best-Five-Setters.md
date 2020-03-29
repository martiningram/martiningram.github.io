---
layout: post
title: Grand Slam five-setters to watch
---

{% include mathjax.html %}

Much like [Steph Kovalchik did a few days ago](http://on-the-t.com/2020/03/26/atp-best-matches/), now that there is no live tennis I found myself wondering which historical matches to watch. We both developed approaches to pick the most interesting ones, and I think the results are different enough that I thought I'd put my selection up too.

The way I decided to go about it was to rank matches by players' combined Elo rating. I fit an [Elo model](https://en.wikipedia.org/wiki/Elo_rating_system) that takes into account surface skill differences as well as the margin of victory as measured by the game spread (perhaps more on that in a future post). I then summarise each match by the total rating. One slight technical detail: because the spread of ratings is different across the different surfaces in my version of Elo, a rating of 2400 on clay would be less impressive than the same value on hard courts. I therefore rank matches based on the [z-score](https://en.wikipedia.org/wiki/Standard_score) of their total Elo, which takes the spread of the ratings into account. For example, if one player has a rating of 2400 and the other has a rating of 2200, and the standard deviation of ratings is 100, I would compute the z-score as $\frac{(2400 - 1500) + (2200 - 1500)}{\sqrt{100^2 + 100^2}}=11.3$, whereas if the standard deviation is 200, this would only produce a z-score of 5.7. I keep only matches that went to five sets and only consider matches from 1980 onwards, since finding matches from before that can be difficult (or, if they exist, their quality is often quite bad).

What kind of matches should this approach pick out? The total Elo skill should tell us something about the quality of the match. If both players have a very high Elo rating, they should both be considerably better than average players, giving the sum of their ratings a high z-score. Keeping only five-setters should go some way towards ensuring that the matches were competitive. With hindsight, I'm not sure that goes far enough: for some matches, perhaps the outcome seemed fairly clear throughout, despite a match going to five. I've been playing with limiting the list to matches where the pre-match gap in ratings was small, but I'm still experimenting with that.

Anyway, without further ado, here's the list (ranked by z-score):

|    | Winner        | Loser           | Tournament   |   Year | Round   | Score                   |   z |   Winner Elo |   Loser Elo |
|---:|:---------------|:-----------------|:------------------|-------:|:--------|:------------------------|----------:|-------------:|------------:|
|  1 | Bjorn Borg     | Ivan Lendl       | Roland Garros     |   1981 | F       | 6-1 4-6 6-2 3-6 6-1     |      15.1 |       2901 |      2402 |
|  2 | John McEnroe   | Bjorn Borg       | US Open           |   1980 | F       | 7-6 6-1 6-7 5-7 6-4     |      14.5 |       2251 |      2551 |
|  3 | John McEnroe   | Jimmy Connors    | US Open           |   1984 | SF      | 6-4 4-6 7-5 4-6 6-3     |      14.1 |       2462 |      2288 |
|  4 | Novak Djokovic | Roger Federer    | US Open           |   2011 | SF      | 6-7(7) 4-6 6-3 6-2 7-5  |      13.9 |       2488 |      2244 |
|  5 | John McEnroe   | Jimmy Connors    | US Open           |   1980 | SF      | 6-4 5-7 0-6 6-3 7-6     |      13   |       2289 |      2328 |
|  6 | Bjorn Borg     | Jimmy Connors    | Wimbledon         |   1981 | SF      | 0-6 4-6 6-3 6-0 6-4     |      13   |       2643 |      2583 |
|  7 | Rafael Nadal   | Novak Djokovic   | Roland Garros     |   2013 | SF      | 6-4 3-6 6-1 6-7(3) 9-7  |      12.9 |       2534 |      2438 |
|  8 | Novak Djokovic | Andy Murray      | Australian Open   |   2012 | SF      | 6-3 3-6 6-7(4) 6-1 7-5  |      12.8 |       2362 |      2228 |
|  9 | Andy Murray    | Novak Djokovic   | US Open           |   2012 | F       | 7-6(10) 7-5 2-6 3-6 6-2 |      12.7 |       2203 |      2374 |
| 10 | Bjorn Borg     | John McEnroe     | Wimbledon         |   1980 | F       | 1-6 7-5 6-3 6-7 8-6     |      12.6 |       2784 |      2382 |
| 11 | Ivan Lendl     | John McEnroe     | Roland Garros     |   1984 | F       | 3-6 2-6 6-4 7-5 7-5     |      12.5 |       2414 |      2502 |
| 12 | John McEnroe   | Mats Wilander    | US Open           |   1985 | SF      | 3-6 6-4 4-6 6-3 6-3     |      12.5 |       2420 |      2133 |
| 13 | Bjorn Borg     | Roscoe Tanner    | US Open           |   1980 | QF      | 6-4 3-6 4-6 7-5 6-3     |      12.4 |       2527 |      2011 |
| 14 | Jimmy Connors  | John McEnroe     | Wimbledon         |   1982 | F       | 3-6 6-3 6-7 7-6 6-4     |      12.3 |       2601 |      2509 |
| 15 | Stan Wawrinka  | Novak Djokovic   | Australian Open   |   2014 | QF      | 2-6 6-4 6-2 3-6 9-7     |      12.2 |       2110 |      2410 |

I found the list pretty striking. Here are some thoughts:

* I hope you're a McEnroe fan because his name comes up _a lot_. He's in 7 of the top 15 matches! The famous Borg - McEnroe 1980 Wimbledon final is on the list, but interestingly, the Borg - McEnroe US Open final of the same year which McEnroe won comes up slightly higher at number 2.  
* Djokovic is popular too, appearing five times. I'm glad the Nadal - Djokovic 2013 French Open made it on the list; I remember watching that and just being in awe at the quality of tennis.
* This method really loves the early 1980s and 2010s: all matches are from one or the other of these eras.
* This model thinks Borg was a _beast_ on clay in 1981. His Elo rating coming into the match against Lendl was 2901! Compare that against Nadal in 2013 against Djokovic, who "only" had a rating of 2534. It actually doesn't seem so crazy when you look at Borg's [record on clay](http://www.tennisabstract.com/cgi-bin/player-classic.cgi?p=BjornBorg&f=ACareerqqB1). This model takes the margin of victory into account and Borg was rarely dropping sets and regularly winning them 6-0. Coming into that match he must have seemed unbeatable, even though he ended up having a tough time against Lendl. That match was to be his last at a French Open.
* I think most people would agree that these are probably good matches. It's perhaps more surprising to note which matches _aren't_ in the list, such as the 2008 Nadal - Federer Wimbledon final. I'll note that this is just one approach, and many subjective choices determine which matches end up at the top.

Personally, I'm looking forward to checking out some of those McEnroe - Connors matches. I hope you get some ideas from reading the list too!

#### Links

1. Borg - Lendl 1981 RG: [link](https://www.youtube.com/watch?v=HGBR04bqago)
2. McEnroe - Borg 1980 US Open: [link](https://www.youtube.com/watch?v=cZKxKWfzUic)
3. McEnroe - Connors 1984 US Open: [link](https://www.youtube.com/watch?v=VRncDRR5xhA)
4. Djokovic - Federer 2011 US Open: I couldn't find the full match sadly but here's a chunk of it: [link](https://www.youtube.com/watch?v=BpO4s99UVCE)
5. McEnroe - Connors 1980 US Open: [link](https://www.youtube.com/watch?v=OcDF08fg21A)
6. Borg - Connors 1981 Wimbledon (sadly fifth set only): [link](https://www.youtube.com/watch?v=Y3ZGXvKbd3A)
7. Nadal - Djokovic 2013 RG (sadly highlights only): [link](https://www.youtube.com/watch?v=9AgTRydkcaI)
8. Djokovic - Murray 2012 AO: [link](https://www.youtube.com/watch?v=3gvCEqz92Qw)
9. Murray - Djokovic 2012 US Open (highlights only): [link](https://www.youtube.com/watch?v=mgVJazH8khA)
10. Borg - McEnroe 1980 Wimbledon (only a part of it): [link](https://www.youtube.com/watch?v=Yf0yfEfvMHE)
11. Lendl - McEnroe 1984 RG: [link](https://www.youtube.com/watch?v=apgMqoXzaCc)
12. McEnroe - Wilander 1985 US Open: [link](https://www.youtube.com/watch?v=kVJhaqI3WfU)
13. Borg - Tanner 1980 US Open: I couldn't find this, sadly!
14. Connors - McEnroe 1982 Wimbledon (highlights only): [link](https://www.youtube.com/watch?v=lApSrH3tWCk)
15. Wawrinka - Djokovic 2014 AO (highlights only): [link](https://www.youtube.com/watch?v=_lvpSguhGvw)
