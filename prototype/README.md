## Summary

This PR contains a copy of the preliminary results data, as well as prototype visualizations of this dataset and the means to reproduce them.  See below for notes about the dataset, a summary of my observations, and a list of questions for further analysis. This content is the precursor for material I would include in a blog post about this data.

## Dataset Notes

The preliminary results dataset ("classifications-prelim.csv") originally included the columns now called: `TwitterUser`, `CategoryOrig`, `Average of pred_prob_0`, and `StdDev of pred_prob_0`. Based on the user names (e.g. "Washington Post"), I conducted Internet searches to populate some additional labels (`TwitterHandle`, `ImageURL`,`UserAffiliation`, `CategoryCustom`). In some cases I made reasonable assumptions about the primary handle or affiliation, so we'll definitely want to revisit these.

## Observations

For most users included in the analysis, their **relative position** on the spectrum of bias scores matches around where I would rank them. For example, as expected, "Breitbart News" is near the bottom and "Jim Acosta" is near the top:

![All](https://user-images.githubusercontent.com/1328807/65727479-d88e7e00-e085-11e9-8800-1ee5b1180122.png)

However, if 0 represents lack of bias and 1 represents bias, the **absolute scores** skew farther above 0.50 than I would have expected (see questions section below). So, while we should be careful to not say any score above 0.50 represents presence of an anti-Trump bias, we can still compare the users' scores relative to each other.

In terms of newspaper and print media accounts, "USA Today" and "The Economist" have the lowest bias scores, while the "Washington Post" has the highest anti-Trump score of the group:

![By Category - Newspaper](https://user-images.githubusercontent.com/1328807/65728220-48056d00-e088-11e9-809b-df63b3440041.png)

Among TV and radio network accounts, as expected, "Fox News" has the lowest anti-Trump score and "MSNBC" has the highest anti-Trump bias. Among the remaining pack, "ABC" and "CBS" are near the bottom of the bias spectrum, while "NPR" and "PBS Newshour" are near the top:

![By Category - TV](https://user-images.githubusercontent.com/1328807/65728215-450a7c80-e088-11e9-86fa-4cb8a2a95f7f.png)

The TV network accounts themselves seem to have a less extreme average predicted bias than their individual contributors, with the exception of "CNN" which seems to be in the middle of its contributors:

![By Network Affiliation](https://user-images.githubusercontent.com/1328807/65727506-e8a65d80-e085-11e9-9080-5847ecfa6cb2.png)

## Outstanding Questions

  1. What exactly is the definition of "bias" as it relates to this data? Does it simply mean the tweet content is likely to be anti-Trump? My initial thought was the word "bias" has connotations that are potentially too strong, but then I looked up the [definition](https://www.merriam-webster.com/dictionary/bias) of the word, and it says "an inclination of temperament or outlook" and "deviation of the expected value of a statistical estimate from the quantity it estimates", so I guess the word may be appropriate.

  2. What is the middle between bias and lack of bias? Mathematically, if 0 represents lack of bias and 1 represents bias, the middle value would be 0.5, but "Fox News" is at 0.57, so does it make sense to say they have a positive anti-Trump bias? Likely no. So the middle value must be higher. Based on the data it looks like it could be around 0.62%. This requires further investigation.
    a. In order to help us understand this phenomenon better, I wonder: what were the predicted anti-Obama results for these same accounts during the Obama presidency? It is possible these anti-Obama values could help us explain where the middle is.

  3. Do low predicted anti-Trump bias values indicate the inverse (a high pro-Trump bias)? Or should we not be reading that way? Obama numbers might help answer this.

  4. How to interpret the standard deviations, which seem large?

Average of pred_prob_0 | StdDev of pred_prob_0
-- | --
0.425558786 | 0.242680134
0.857377488 | 0.28998357
0.836335689 | 0.294347562
... | ...
0.584096035 | 0.417727874
0.57209972 | 0.418222037
0.385370163 | 0.421144792

  5. What are some example tweets that have been classified at high / low bias? I'd want to include a few in the blog post.

  6. FUTURE: Is it possible to create another classifier for the TV programming itself? Using transcripts, etc.
