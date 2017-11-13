


# Visualizing proportions {#visualizing-proportions}

We often want to show how some group, entity, or amount breaks down into individual pieces that each represent a *proportion* of the whole. Common examples include the proportions of men and women in a group of people, the percentages of people voting for different political parties in an election, or the market shares of companies. The archetypical such visualization is the pie chart, omnipresent in any business presentation and much maligned among data scientists. As we will see, visualizing proportions can be challenging, in particular when the whole is broken into many different pieces or when we want to see changes in proportions over time or across conditions. There is no single ideal visualization that always works. To illustrate this issue, I discuss a few different scenarios that each call for a different type of visualization.

<div class="rmdtip">
<p>Remember: You always need to pick the visualization that best fits your specific dataset and that highlights the key data features you want to show.</p>
</div>


## A case for pie charts

From 1961 to 1983, the German parliament (called the *Bundestag*) was composed of members of three different parties, CDU/CSU, SPD, and FDP. During most of this time, CDU/CSU and SPD had approximately comparable numbers of seats, while the FDP typically held only a small fraction of seats. For example, in the 8th Bundestag, from 1976--1980, the CDU/CSU held 243 seats, SPD 214, and FDP 39, for a total of 496. Such parliamentary data is most commonly visualized as a pie chart (Figure \@ref(fig:bundestag-pie)).

(ref:bundestag-pie) Party composition of the 8th German Bundestag, 1976--1980, visualized as a pie chart. This visualization shows clearly that the ruling coalition of SPD and FDP had a small majority over the opposition CDU/CSU.

<div class="figure" style="text-align: center">
<img src="visualizing_proportions_files/figure-html/bundestag-pie-1.png" alt="(ref:bundestag-pie)" width="403.2" />
<p class="caption">(\#fig:bundestag-pie)(ref:bundestag-pie)</p>
</div>

A pie chart breaks a circle into slices such that the area of each slice is proportional to the fraction of the total it represents. The same procedure can be performed on a rectangle, and the result is a stacked bar chart (Figure \@ref(fig:bundestag-stacked-bars)). Depending on whether we slice the bar vertically or horizontally, we obtain vertically stacked bars (Figure \@ref(fig:bundestag-stacked-bars)a) or horizontally stacked bars (Figure \@ref(fig:bundestag-stacked-bars)b).

(ref:bundestag-stacked-bars) Party composition of the 8th German Bundestag, 1976--1980, visualized as stacked bars. (a) Bars stacked vertically. (b) Bars stacked horizontally. It is not immediately obvious that SPD and FDP jointly had more seats than CDU/CSU.

<div class="figure" style="text-align: center">
<img src="visualizing_proportions_files/figure-html/bundestag-stacked-bars-1.png" alt="(ref:bundestag-stacked-bars)" width="816" />
<p class="caption">(\#fig:bundestag-stacked-bars)(ref:bundestag-stacked-bars)</p>
</div>

We can also take the bars from Figure \@ref(fig:bundestag-stacked-bars)a and place them side-by-side rather than stacking them on top of each other. This visualization makes it easier to perform a direct comparison of the three groups, though it obscures other aspects of the data (Figure \@ref(fig:bundestag-bars-side-by-side)). Most importantly, in a side-by-side bar plot the relationship of each bar to the total is not visually obvious.

(ref:bundestag-bars-side-by-side) Party composition of the 8th German Bundestag, 1976--1980, visualized as side-by-side bars. As in Figure \@ref(fig:bundestag-stacked-bars), it is not immediately obvious that SPD and FDP jointly had more seats than CDU/CSU.

<div class="figure" style="text-align: center">
<img src="visualizing_proportions_files/figure-html/bundestag-bars-side-by-side-1.png" alt="(ref:bundestag-bars-side-by-side)" width="576" />
<p class="caption">(\#fig:bundestag-bars-side-by-side)(ref:bundestag-bars-side-by-side)</p>
</div>

Many authors categorically reject pie charts and argue in favor of side-by-side or stacked bars. Others defend the use of pie charts in some applications. My own opinion is that none of these visualizations is consistently superior over any other. Depending on the features of the dataset and the specific story you want to tell, you may want to favor one or the other approach. In the case of the 8th German Bundestag, I think that a pie chart is the best option. It shows clearly that the ruling coalition of SPD and FDP jointly had a small majority over the CDU/CSU (Figure \@ref(fig:bundestag-pie)). This fact is not visually obvious in any of the other plots (Figures \@ref(fig:bundestag-stacked-bars) and \@ref(fig:bundestag-bars-side-by-side)). 

In general, pie charts work well when the goal is to emphasize simple fractions, such as one-half, one-third, or one-quarter. They also work well when we have very small datasets. A single pie chart, as in Figure \@ref(fig:bundestag-pie), looks just fine, but a single column of stacked bars, as in Figure \@ref(fig:bundestag-stacked-bars)a, looks awkward. Stacked bars, on the other hand, can work for side-by-side comparisons of multiple conditions or in a time series, and side-by-side bars are preferred when we want to directly compare the individual fractions to each other. A summary of the various pros and cons of pie charts, stacked bars, and side-by-side bars is provided in Table \@ref(tab:pros-cons-pie-bar). 

Table: (\#tab:pros-cons-pie-bar) Pros and cons of common apporaches to visualizing proportions: pie charts, stacked bars, and side-by-side bars. 

----------------------------------------------------------------------------------------
                                    Pie chart         Stacked bars      Side-by-side bars
-----------------------------  ------------------- ------------------- -------------------
Clearly visualizes the data             ✔                 ✔                   ✖
as proportions of a whole

Allows easy visual comparison           ✖                 ✖                   ✔ 
of the relative proportions 

Visually emphasizes simple              ✔                 ✖                   ✖
fractions, such as 1/2, 1/3,
1/4

Looks visually appealing                ✔                 ✖                   ✔
even for very small datasets

Works well when the whole is            ✖                 ✖                   ✔ 
broken into many pieces

Works well for the                      ✖                 ✔                   ✖
visualization of many sets of
proportions or time series
of proportions
----------------------------------------------------------------------------------------


## A case for side-by-side bars {#side-by-side-bars}

I will now demonstrate a case where pie charts fail. This example is modeled after a critiqute of pie charts originally posted on Wikipedia [@Schutz-piecharts]. Consider the hypothetical scenario of five companies, A, B, C, D, and E, who all have roughly comparable market share of approximately 20%. Our hypothetical dataset lists the marketshare of each company for three consecutive years. When we visualize this dataset with pie charts, it is difficult to see what exactly is going on (Figure \@ref(fig:marketshare-pies)). It appears that the market share of company A is growing and the one of company E is shrinking, but beyond this one observation we can't tell what's going on. In particular, it is unclear how exactly the market shares of the different companies compare within each year.




(ref:marketshare-pies) Market share of five hypothetical companies, A--E, for the years 2015--2017, visualized as pie charts. This visualization has two major problems: 1. A comparison of relative market share within years is nearly impossible. 2. Changes in market share across years are difficult to see.

<div class="figure" style="text-align: center">
<img src="visualizing_proportions_files/figure-html/marketshare-pies-1.png" alt="(ref:marketshare-pies)" width="816" />
<p class="caption">(\#fig:marketshare-pies)(ref:marketshare-pies)</p>
</div>

The picture becomes a little clearer when we switch to stacked bars (Figure \@ref(fig:marketshare-stacked)). Now the trends of a growing market share for company A and a shrinking market share for company E are clearly visible. However, the relative market shares of the five companies within each year are still hard to compare. And it is difficult to compare the market shares of companies B, C, and D across years, because the bars are shifted relative to each other across years. This is a general problem of stacked-bar plots, and the main reason why I normally not recommend this type of visualization.

(ref:marketshare-stacked) Market share of five hypothetical companies for the years 2015--2017, visualized as stacked bars. This visualization has two major problems: 1. A comparison of relative market shares within years is difficult. 2. Changes in market share across years are difficult to see for the middle companies B, C, and D, because the location of the bars changes across years.

<div class="figure" style="text-align: center">
<img src="visualizing_proportions_files/figure-html/marketshare-stacked-1.png" alt="(ref:marketshare-stacked)" width="576" />
<p class="caption">(\#fig:marketshare-stacked)(ref:marketshare-stacked)</p>
</div>

For this hypothetical data set, side-by-side bars are the best choice (Figure \@ref(fig:marketshare-side-by-side)). This visualization highlights that both companies A and B have increased their market share from 2015 to 2017 while both companies D and E have reduced theirs. It also shows that market shares increase sequentially from company A to E in 2015 and similarly decrease in 2017.

(ref:marketshare-side-by-side) Market share of five hypothetical companies for the years 2015--2017, visualized as side-by-side bars.

<div class="figure" style="text-align: center">
<img src="visualizing_proportions_files/figure-html/marketshare-side-by-side-1.png" alt="(ref:marketshare-side-by-side)" width="576" />
<p class="caption">(\#fig:marketshare-side-by-side)(ref:marketshare-side-by-side)</p>
</div>


## A case for stacked bars and stacked densities

In Section \@ref(side-by-side-bars), I wrote that I don't normally recommend sequences of stacked bars, because the location of the internal bars shifts along the sequence. However, the problem of shifting internal bars disappears if there are only two bars in each stack, and in those cases the resulting visualization can be exceptionally clear. As an example, consider the proportion of women in a country's national parliament. We will specifically look at the African country Rwanda, which as of 2016 tops the list of countries with the highest proportion of female parliament memebers. Rwanda has had a majority female parliament since 2008, and since 2013 nearly two-thirds of its members of parliament are female. To visualize how the proportion of women in the Rwandan parliament has changed over time, we can draw a sequence of stacked bar graphs (Figure \@ref(fig:women-parliament)). This figure provides an immediate visual representation of the changing proportions over time. To help the reader see exactly when the majority turned female, I have added a thin horizontal line at 50%. Without this line, it would be near impossible to determine whether from 2003 to 2007 the majority was male or female. I have not added similar lines at 25% and 75%, to avoid making the figure too cluttered. (See Chapter \@ref(background-grids) for further discussion on such lines.)

(ref:women-parliament) Change in the gender composition of the Rwandan parliament over time, 1997 to 2016. Source: Inter-Parliamentary Union (IPU), ipu.org.

<div class="figure" style="text-align: center">
<img src="visualizing_proportions_files/figure-html/women-parliament-1.png" alt="(ref:women-parliament)" width="720" />
<p class="caption">(\#fig:women-parliament)(ref:women-parliament)</p>
</div>

If we want to visualize how proportions change in response to a continuous variable, we can switch from stacked bars to stacked densities. Stacked densities can be thought of as the limiting case of infinitely many infinitely small stacked bars arranged side-by-side. The densities in stacked-density plots are typically obtained from kernel density estimation, as described in Chapter \@ref(histograms-density-plots), and I refer you to that chapter for a general discussion of the strengths and weaknesses of this method.

To give an example where stacked densities are appropriate, consider the health status of people as a function of age. Age can be considered a continuous variable, and visualizing the data this way works well (Figure \@ref(fig:health-vs-age)). Even though we have four health categories here, and I'm generally not a fan of stacking multiple conditions, as discussed above, I think in this case the figure works. We can see clearly that overall health declines as people age, and we can also see that despite this trend, over half of the population remain in good or excellent health until very old age.

(ref:health-vs-age) Health status by age, as reported by the general social survey (GSS).

<div class="figure" style="text-align: center">
<img src="visualizing_proportions_files/figure-html/health-vs-age-1.png" alt="(ref:health-vs-age)" width="720" />
<p class="caption">(\#fig:health-vs-age)(ref:health-vs-age)</p>
</div>

For an example, see Section \@ref(multiple-histograms-densities) in Chapter \@ref(histograms-density-plots).


**Additional ideas for this chapter: nested proportions, treemaps and Sankey diagrams.**

