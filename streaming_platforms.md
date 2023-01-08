Case Study of Four Streaming Service Platforms
================
Suhail Torga
2023-01-07

### Introduction

In the last few years, the amount of streaming service platforms has
increased significantly. Each claims to have the best movies and shows
that can cover any audience’s preferences. However, with so many options
it becomes difficult to decide which streaming platform offers the best
deal. For this very reason, I decided to come up with a data analysis of
the top 4 streaming platforms for general audiences: [Prime
Video](https://www.primevideo.com/), [HBO Max](https://www.hbomax.com),
[Netflix](https://www.netflix.com) and [Paramount
Plus](https://www.paramountplus.com). As I have already tried
[Disney+](https://www.disneyplus.com) and
[Star+](https://www.starplus.com) and decided that their selection isn’t
something that interests me much, I decided against adding them to the
study.

After giving it much thought, I came up with 5 questions which will be
discussed in detail in the following sections. Their aim is to determine
what each streaming service platform offers and, thus, help audiences
determine which one they prefer based on what they are looking for.

- *Section 1: Limitations of the study*
- *Section 2: Platform with the most recent released titles*
- *Section 3: Audiences being targeted*
- *Section 4: Most popular genres*
- *Section 5: Correlation between IMDb and TMDB scores*
- *Section 6: Amount of titles scoring good marks*
- *Section 7: Key takeaways from the case study*

May the results obtained in this case study help others make informed
decisions about which streaming service platform interests them the
most.

### Section 1: Limitations of the study

As previously mentioned, this study will only focus on the following
platforms:

- [Prime Video](https://www.primevideo.com/)
- [HBO Max](https://www.hbomax.com)
- [Netflix](https://www.netflix.com)
- [Paramount Plus](https://www.paramountplus.com)

As such, the study is limited to a handful of options.

Now, in terms of the actual data provided in the data sets obtained from
[Kaggle](https://www.kaggle.com/datasets), there are missing values
found within the columns for IMDb and TMDB Scores, which determine how
critics and audiences rate the movies and shows and which will be
discussed in *Section 5*.

The amount of data missing with regards to the total number of entries
is as follows:

![FIGURE 1: Missing scores for IMDb and TMDB
Scores](./figs/missing_scores_percentages.png)

In Figure 1, it can be clearly seen that HBO Max has the data set with
the largest percentage of missing IMDb (Critic) Scores, while Amazon
Prime (Prime Video) holds the top position for missing data in the TMDB
(Audience) Scores column. However, once the missing data in both columns
is combined, the numbers tell a different story:

![FIGURE 2: Combined percentages of missing
data](./figs/missing_total_scores.png)

In Figure 2, it is clear that Amazon Prime holds the top position in
terms of overall missing data, which might not seem as much, but that
can have an effect in calculations. *Section 5* will cover to what
extent these missing data may or may not have an impact.

### Section 2: Platform with the most recent released titles

It is true that there are some classics out there, which most people
enjoy watching over and over again. However, adding new releases to
their selection helps streaming platforms remain current and attractive.
After all, most audiences like novelty and want to stay up-to-date with
the most current movies and shows.

Below, in Figure 3, all four platforms are shown with the amount of
titles that have been released after 2020.

![FIGURE 3: Number of titles released after 2020 by
platform](./figs/titles_released_2020.png)

Figure 3 shows that both Amazon Prime and Netflix far surpass the other
two streaming platforms in terms of the amount of titles that have been
released since 2020. This may also be a direct result of the fact that
both of these streaming platforms invest heavily on producing and
releasing original shows and movies around the globe.

### Section 3: Audiences being targeted

Another interesting point that must be considered when choosing a
streaming platform is understanding who their target audience is. This
is important as it tells the type of material that we are most likely
going to find in their platforms, and whether they might be of interest
to us.

The [Motion Picture Association film rating
system](https://en.wikipedia.org/wiki/Motion_Picture_Association_film_rating_system)
is used in the United States for restricting movies that may only be
viewed by audiences depending on their age. As for TV shows, the [TV
Parental
Guidelines](https://en.wikipedia.org/wiki/TV_Parental_Guidelines) is
used to determine age-appropriate content for audiences in the United
States. In all four platform data sets, both of these rating systems are
used to rate each entry. For this reason, the

``` r
lapply(streaming_service, function(x) x %>% 
         group_by(age_certification) %>% 
         summarise(titles=length(age_certification))) 
```

    ## $AmazonPlatform
    ## # A tibble: 12 × 2
    ##    age_certification titles
    ##    <chr>              <int>
    ##  1 G                    269
    ##  2 NC-17                 13
    ##  3 PG                   582
    ##  4 PG-13                588
    ##  5 R                   1249
    ##  6 TV-14                188
    ##  7 TV-G                  57
    ##  8 TV-MA                217
    ##  9 TV-PG                 91
    ## 10 TV-Y                  78
    ## 11 TV-Y7                 52
    ## 12 <NA>                6487
    ## 
    ## $HBOMaxPlatform
    ## # A tibble: 12 × 2
    ##    age_certification titles
    ##    <chr>              <int>
    ##  1 ""                  1208
    ##  2 "G"                   83
    ##  3 "NC-17"                7
    ##  4 "PG"                 308
    ##  5 "PG-13"              470
    ##  6 "R"                  597
    ##  7 "TV-14"              146
    ##  8 "TV-G"                20
    ##  9 "TV-MA"              313
    ## 10 "TV-PG"               84
    ## 11 "TV-Y"                17
    ## 12 "TV-Y7"               41
    ## 
    ## $NetflixPlatform
    ## # A tibble: 12 × 2
    ##    age_certification titles
    ##    <chr>              <int>
    ##  1 ""                  2619
    ##  2 "G"                  124
    ##  3 "NC-17"               16
    ##  4 "PG"                 233
    ##  5 "PG-13"              451
    ##  6 "R"                  556
    ##  7 "TV-14"              474
    ##  8 "TV-G"                79
    ##  9 "TV-MA"              883
    ## 10 "TV-PG"              188
    ## 11 "TV-Y"               107
    ## 12 "TV-Y7"              120
    ## 
    ## $ParamountPlatform
    ## # A tibble: 12 × 2
    ##    age_certification titles
    ##    <chr>              <int>
    ##  1 ""                  1523
    ##  2 "G"                   90
    ##  3 "NC-17"                3
    ##  4 "PG"                 147
    ##  5 "PG-13"              180
    ##  6 "R"                  321
    ##  7 "TV-14"              165
    ##  8 "TV-G"                95
    ##  9 "TV-MA"               56
    ## 10 "TV-PG"              143
    ## 11 "TV-Y"                50
    ## 12 "TV-Y7"               52

In each of the tables above, the first entry “” signifies that the title
didn’t get a rating. In the case of Amazon Prime the missing data is
represented by the last entry of the table with the letters NA. In
either case, this may have been a mistake carried out by the people who
compiled the data set or it might mean that none of the platforms have
assigned the appropriate age-restriction settings. Whatever the case may
be, we can still take a look at the rest of the ratings to get a sense
of which audience is mostly being targeted, without forgetting that we
are assuming that the missing values are evenly distributed across the
rest of the rating letters.

- In the case of Amazon Prime, we can clearly see that a big chunk of
  their material is geared towards an audience 17 and above
  (*R-restricted: 1249 titles*).
- In contrast, HBO Max has a more evenly distributed rating accross *PG:
  308 titles*, *PG-13: 470 titles* and *R: 597 titles*, meaning that
  their content targets most audiences, except young children.
- As for Netflix, their shows heavily target mature audiences
  (*TV-MA:883 titles*), while their movies try to bring in younger
  audiences without ignoring their already adult captive audience
  (*PG-13: 451 titles* and *R: 556 titles*).
- Finally, Paramount Plus also has a significant emphasis on mature
  audiences (*R:321*).

This was a very general overview of what the content of each platform
looks like. It is by no means a thorough statistical analysis as this
would entail further exploration, which at the time of this study would
be severely hindered by the amount of missing data missing in both
movies and tv shows.

### Section 4: Most popular genres

No study focused on streaming services would be complete without
addressing the genres that each platform provides for their audiences.
After all, we all have our particular tastes when it comes to the genres
that most appeal to us. In my case, I tend to go for comedy and fantasy,
which I find most entertaining and light-hearted.

In order to avoid data overload, each platform was analyzed
independently, as there are many genres contained in each data set, and
joining all four data sets would have led to a monstrosity of a graphic.

![FIGURE 4: Amazon Prime genre
preference](./figs/amazon_genre_preference.png)

![FIGURE 5: HBO Max genre
preference](./figs/hbomax_genre_preference.png)

![FIGURE 6: Netflix genre
preference](./figs/netflix_genre_preference.png)

![FIGURE 7: Paramount Plus genre
preference](./figs/paramount_genre_preference.png)

Before discussing what each of the above four graphs is telling us, it
must be noted that many titles have several genres assigned to them. For
this very reason, the amount titles contained in each platform is lower
to the total sum of each genre per platform. Having said that, we can
now proceed to taking a closer look to what the data is telling us:

- Figures 4 through 7 show that *Comedy* and *Drama* are the top genres
  that each platform targets. Though no survey results were provided to
  determine whether audiences truly prefer these 2 genres, it is clear
  that all platforms believe this to be the case.
- Most all other genres are well-below the other two, with a distinct
  and contrasting distribution across platforms.

Because of this last observation, it comes down to personal preference
as to which platform offers. In my case, *Comedy* and *Fantasy*, as a I
mentioned before, are my personal preferences. Since the former is
highly targeted by all four platforms, it comes down to taking a look at
which platform offers the most amount of titles to determine whether it
is a platform that fulfills my preferences. Taking this into account, it
seems Netflix *with 630 titles* makes the obvious choice, closely
followed by Amazon Prime *with 554 titles*. Readers are encouraged to
compare how their own preferences weigh up to what each platform offers.

### Section 5: Correlation between IMDb and TMDB scores

Oftentimes, people turn to critics and other audience opinions about
what movie or show might be worth watching. I, myself, have done this
from time to time. However, it is true that critics and audience members
don’t always see eye to eye. That being the case, it is the aim of this
section to determine whether IMDb (critic) and TMDB (audience) scores
share any correlation to each other.

Below are the scatter plots of each platform with their respective
linear regressions.

![FIGURE 8: IMDb and TMDB scores for Amazon
Prime](./figs/amazon_correlation.png)

![FIGURE 9: IMDb and TMDB scores for HBO
Max](./figs/hbomax_correlation.png)

![FIGURE 10: IMDb and TMDB scores for
Netflix](./figs/netflix_correlation.png)

![FIGURE 11: IMDb and TMDB scores for Paramount
Plus](./figs/paramount_correlation.png)

In Figures 8 through 11, each scatter plot seems to be showing some sort
of visual pattern with an upward trend. However, once a statistical
approach is taken, this notion is shattered. In all of the above
scatter plots, two values of the linear regression are being displayed:
*R-squared value* and *P-value*. Each of these values tells us how
strongly related the two variables are. The P-value tells us how
significant the results are. Anything below 0.001 is quite significant.
Yet R-squared values tell the whole story. First, they fluctuate between
0 and 1. The closer the value is to zero, the weaker the correlation
is. The further away from zero the R-squared value
is, the stronger the correlation. Unfortunately, the correlation in all
four cases was very weak, which meant that critic scores DO NOT explain
what audience scores will be. That means that readers must be careful
when listening to what critics say as these are not a clear indicative
of what audience members will most likely appreciate.

### Section 6: Amount of titles scoring good marks

The reason why this last section was included is because I believe that
no matter how many titles each platform makes available to their
audiences, good scores are what will determine if their movies and shows
are worth taking a look at or not.

But before we dive into the actual results, it is important that we look
at how many titles each platform has so that we make a more significant
comparison.

``` r
lapply(streaming_service, function(x) nrow(x))
```

    ## $AmazonPlatform
    ## [1] 9871
    ## 
    ## $HBOMaxPlatform
    ## [1] 3294
    ## 
    ## $NetflixPlatform
    ## [1] 5850
    ## 
    ## $ParamountPlatform
    ## [1] 2825

In the list above, we can see that Amazon Prime *with 9871 titles* way
surpasses the other three platforms in terms of the sheer amount of
titles it has. With this in mind, it now makes sense to proceed and look
at the number of titles receiving good scores by both critics (*IMDb
Scores*) and audience members (*TMDB Scores*). The scores go from 0 to 10 
and, thus, the cutoff was set at 8.0 as this provides a strict requisite
without being impossible to reach by most movies and shows.

The results are shown below:

![FIGURE 12: Titles with IMDb and TMDB socres above
8.0](./figs/popularity_above_8.png)

Figure 12 clearly shows that for both IMDb and TMDB scores Netflix holds
the highest number of entries above 8.0 even though it holds 3021 less
movies and shows than Amazon Prime, which has the largest selection.
This goes to show that Amazon Prime doesn’t have the best selection of
titles as perceived by both critics and audience in general. However, it
must be noted that HBO Max closely followed Netflix in terms of titles
well-liked by the critics, even though it has 1556 less titles overall
than Netflix does. So, it can be concluded that the best
critic-acclaimed movies and shows can be found in Netflix and HBO Max as
opposed to the other two platforms. Sadly, Paramount Plus holds the last
position for both critic-and-audience-acclaimed titles, which make it a
poor platform when compared to the other three.

### Section 7: Key takeaways from the case study

In general, it can be concluded that each platform has something to
offer their audiences. However, aside from Paramount Plus which scored
the lowest in all of the different categories, each one shines in their
own particular way:

- Amazon Prime has the largest selection of movies and shows with a high
  emphasis on R-rated titles geared towards adult audiences.
- HBO Max has a more evenly distributed number of titles geared towards
  most audiences except children.
- Netflix has the highest number of titles released after 2020 as well
  as the largest selection of movies and shows which received both
  critic and audience scores higher than 8.0.
- All platforms focus on two main genres: *Drama* and *Comedy*.
- Critic opinions DO NOT translate well into what audiences consider are
  good movies and shows.

With these results in mind, it is my hope that readers feel better
equipped to make well-informed decisions as to which platform is more to
their liking and which ones they should stay away from.
