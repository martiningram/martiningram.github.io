---
layout: post
title: US Open Elo preview
---

{% include image.html url="/images/novak_uso_smaller.jpg" description="<i>Novak Djokovic
at the US Open. Image credit: Getty Images</i>" %}

I'm a little bit late (the first round has already started!), but I wanted to briefly write about the ratings I have for this year's US Open. These ratings are based on a new variant of Elo I've been working on which takes into account surface effects, margin of victory, retirements, the format (best of five / best of three), and slam effects. They're still a bit experimental, but they seem to improve predictions overall. Of course, with the coronavirus pandemic disrupting most of this season, there is probably even more uncertainty in forecasting than usual, but I am not taking this into account here.

On the men's side, here are the 16 highest-ranked players. The columns show their hard-court Elo ratings, the estimated slam addition, and their total rating:

|                             |   Hard |   Slam+ |   Total |
|:----------------------------|-------:|--------:|--------:|
| 1.  Novak Djokovic              |   2201 |      42 |    2243 |
| 2.  Stefanos Tsitsipas          |   1982 |      -8 |    1974 |
| 3.  Milos Raonic                |   1916 |      10 |    1927 |
| 4.  Daniil Medvedev             |   1923 |     -11 |    1911 |
| 5.  Roberto Bautista Agut       |   1905 |       5 |    1910 |
| 6.  Andrey Rublev               |   1877 |      11 |    1887 |
| 7.  Dominic Thiem               |   1832 |      35 |    1867 |
| 8.  Alexander Zverev            |   1874 |     -16 |    1858 |
| 9.  <s>Diego Sebastian Schwartzman</s> |   1802 |      25 |    1827 |
| 10. Jan-Lennard Struff          |   1816 |       4 |    1819 |
| 11. Alex De Minaur              |   1797 |       4 |    1801 |
| 12. Filip Krajinovic            |   1816 |     -17 |    1798 |
| 13. David Goffin                |   1791 |       6 |    1797 |
| 14. Matteo Berrettini           |   1794 |       2 |    1796 |
| 15. Andy Murray                 |   1771 |      23 |    1794 |
| 16. Denis Shapovalov            |   1776 |      10 |    1786 |

I don't think there are too many surprises here. Novak leads the field by a large margin and is the clear favourite. He's almost 300 points clear of Stefanos Tsitsipas, who comes in second. Djokovic and Thiem have the highest slam additions, and Krajinovic and Zverev lose a few points (-17 and -16). Raonic is third on account of his run to the finals in Cincinnati, but Medvedev and Bautista Agut aren't far behind. I've crossed out Diego Schwartzman, who has already lost to Norrie.

Thiem's ranking is perhaps a little low, but I suspect it's a consequence of his relatively poor showings at the Rio Open (lost in the quarters) and in Cincinnati (where he lost 6-2 6-1 to Krajinovic). I also discard exhibitions, which I think is generally a good idea, but his performances there have been quite good, which might weigh in his favour somewhat. It could be that the model is reading too much into his last result against Krajinovic.

Overall, it's going to be Novak vs. the rest. I'm really curious to see what will happen!

Here's the situation on the women's side:

|                   |   Hard |   Slam+ |   Total |
|:------------------|-------:|--------:|--------:|
| 1.  Serena Williams   |   1916 |     125 |    2041 |
| 2.  Elise Mertens     |   1959 |      54 |    2013 |
| 3.  Naomi Osaka       |   1950 |      54 |    2005 |
| 4.  Garbine Muguruza  |   1890 |      89 |    1979 |
| 5.  Petra Kvitova     |   1935 |      25 |    1961 |
| 6.  Karolina Pliskova |   1928 |      -9 |    1919 |
| 7.  Aryna Sabalenka   |   1922 |      -9 |    1913 |
| 8.  Madison Keys      |   1851 |      44 |    1896 |
| 9.  Anett Kontaveit   |   1887 |       8 |    1895 |
| 10. Johanna Konta     |   1878 |      15 |    1893 |
| 11. Victoria Azarenka |   1846 |      40 |    1886 |
| 12. Ons Jabeur        |   1853 |      29 |    1883 |
| 13. Jennifer Brady    |   1855 |       7 |    1862 |
| 14. Kim Clijsters*    |   1824 |      27 |    1852 |
| 15. Sofia Kenin       |   1827 |      24 |    1851 |
| 16. Karolina Muchova  |   1821 |      21 |    1842 |

This list has a few more surprises. Firstly, the model estimates that slam effects are considerably larger on the women's side, which is interesting. This propels Serena Williams to the top of the list. I'm really not sure about this -- I'd rate her much lower personally given her recent performances -- but it does seem to be consistent with the betting markets, who also have Osaka and Williams as favourites. On the other hand, Clijsters at 14 seems obviously problematic. She's only played two matches this year, so I think it's unlikely that the ratings have adjusted enough, and I'm giving her an asterisk.

_Unlike_ the betting markets, these ratings seem to like Mertens' chances. She did have a good run in Cincinnati and Prague, so I don't think this is too crazy, and it'll be interesting to keep an eye on her.

Overall, the field for the women is much more crowded, with no standout favourite. Lots of players come with question marks. Just to list a few: Serena may be rated too highly, Mertens has never won a slam, Osaka retired in Cincinnati, Muguruza hasn't played since February, Kvitova and Pliskova lost in the first round of Cincinnati... It'll be fascinating to see who can separate themselves from the rest and win this year.

All in all, I hope you find this quick look at the ratings interesting, and I'm curious to see how well they hold up over the course of the tournament!
