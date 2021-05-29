---
layout: post
title: Surface-adjusted French Open seedings
---

{% include image.html url="/images/rafa_eyebrow.jpg" description="<i>What I
imagine Nadal's reaction to this year's seedings might look like</i>" %}

The French Open is right around the corner and it has really highlighted some of
the issues with the tournament's seeding. Seeding is based on the ATP rankings,
but as any tennis fan knows, some players prefer clay more than others. This is
most striking for Daniil Medvedev who is, incredibly, seeded second _ahead of
13-time winner Nadal_ even though he has never got past the first round in the
tournament.

In this quick post, I compare the tournament seedings against what a rating system with surface effects would predict (in this case [a slightly tweaked GenElo computed with the jax_elo package](https://github.com/martiningram/jax_elo)). The following table shows the 32 highest-ranked players according to the surface-specific GenElo ratings, which takes into account margin of victory, surface, and also slam effects. It also lists the tournament seedings, and which half of the draw the player is in:


| Name                        | GenElo Rank | GenElo clay+slam rating | Tournament seeding | Draw half |
| :-------------------------- | ----------: | ----------------------: | :----------------- | --------- |
| Rafael Nadal                |           1 |                    2875 | 3                  | Top       |
| Novak Djokovic              |           2 |                    2838 | 1                  | Top       |
| Stefanos Tsitsipas          |           3 |                    2808 | 5                  | Bottom    |
| Alexander Zverev            |           4 |                    2626 | 6                  | Bottom    |
| Matteo Berrettini           |           5 |                    2585 | 9                  | Top       |
| Casper Ruud                 |           6 |                    2554 | 15                 | Bottom    |
| Andrey Rublev               |           7 |                    2550 | 7                  | Top       |
| Pablo Carreno-Busta         |           8 |                    2494 | 12                 | Bottom    |
| Aslan Karatsev              |           9 |                    2462 | 24                 | Top       |
| Dominic Thiem               |          10 |                    2447 | 4                  | Bottom    |
| Jannik Sinner               |          11 |                    2426 | 18                 | Top       |
| Roger Federer               |          12 |                    2417 | 8                  | Top       |
| Milos Raonic                |          13 |                    2412 | 17                 | Bottom    |
| Sebastian Korda             |          14 |                    2411 | Unseeded           | Bottom    |
| Carlos Alcaraz Garfia       |          15 |                    2408 | Unseeded           | Top       |
| Lorenzo Sonego              |          16 |                    2402 | 26                 | Top       |
| Felix Auger Aliassime       |          17 |                    2394 | 20                 | Top       |
| Cameron Norrie              |          18 |                    2394 | Unseeded           | Top       |
| Roberto Bautista Agut       |          19 |                    2391 | 11                 | Bottom    |
| Kei Nishikori               |          20 |                    2375 | Unseeded           | Bottom    |
| Daniil Medvedev             |          21 |                    2360 | 2                  | Bottom    |
| Christian Garin             |          22 |                    2357 | 22                 | Bottom    |
| Alejandro Davidovich Fokina |          23 |                    2346 | Unseeded           | Bottom    |
| Taylor Harry Fritz          |          24 |                    2343 | 30                 | Top       |
| Diego Sebastian Schwartzman |          25 |                    2332 | 10                 | Top       |
| Albert Ramos-Vinolas        |          26 |                    2330 | Unseeded           | Top       |
| Federico Delbonis           |          27 |                    2328 | Unseeded           | Bottom    |
| Laslo Djere                 |          28 |                    2313 | Unseeded           | Bottom    |
| Carlos Taberner             |          29 |                    2305 | Unseeded           | Bottom    |
| Marton Fucsovics            |          30 |                    2302 | Unseeded           | Bottom    |
| Marco Cecchinato            |          31 |                    2300 | Unseeded           | Top       |
| Grigor Dimitrov             |          32 |                    2289 | 16                 | Bottom    |

It's quite clear that the seedings you would obtain from the surface-adjusted rating are quite different from the ones used by the tournament. Medvedev, discussed previously, is the most obvious case: GenElo has him 21st-ranked, while his seeding is 2.

He's not the only one, though. Some of the top 32 seeds don't even make the GenElo list. Gael Monfils and David Goffin, for example, are seeded 13th and 14th, but don't make the top 32 here. These are two players who have had good results on clay in the past, but for whom the two-year ATP ranking may not have adjusted quickly enough.

I was a little surprised to see Thiem quite low (10th), but his recent results have not been great. His rating was 2,614 at the start of the year, which would have put him in fourth spot, but he has dropped since then.

The most surprising name in the list is probably Carlos Taberner. I haven't actually seen him play yet, but he appears to have crushed his opponents in qualifying, winning 6-1 6-2 over Klizan, 6-2 6-0 over Fabbiano, and 6-1 6-0 over Menezes. He could be fun to keep an eye on.

It's interesting to see that while Nadal _is_ the favourite according to this
algorithm, he's not ahead by much, [something Steph Kovalchik recently found
too](http://on-the-t.com/2021/05/22/Ratings-Gap-Narrowing/). He, Djokovic and
Tsitsipas are still comfortably ahead of the rest of the field however, with
only Zverev really coming even remotely near them.

Finally, Federer is probably overrated by the algorithm, just because he hasn't
played much. If he's physically fit, I think putting him in 12th spot doesn't
seem crazy, but his loss to Andujar in Geneva didn't inspire a great deal of
confidence. His first round against Istomin seems winnable though: Istomin is
rated at 1,993 Elo points, well below any seeded player (for comparison, Andujar
is currently rated at 2,204 points).

I hope you enjoyed this quick look at alternative seedings for the French Open Men's draw. I'll be curious to see how well they hold up!
