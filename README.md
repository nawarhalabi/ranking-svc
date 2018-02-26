# ranking-svc
Using SVC to rank items from pairwise comparisons. Pairwise comparisons are comparisons collected from human annotators (for example) for pairs of items/objects based on a certain quality of these items (which restaurant is better for example based on food quality for example). These pairwise comparisons over a large set of items (restautants) can be used to generate rankings of these restaurants.

![picture alt](https://github.com/nawarhalabi/ranking-svc/blob/master/pairwise2ranking.png "Example of a graph representation of pairwise comparisons and ranks")

This is a demo which conducts a simulation of ranking from these pairwise comparisons using SVCs. the simulation assumes a list of items `[1, 2, 3, ... , N]` which are a ground truth ranking. We observe a partial set of the total `n * ( n - 1 ) / 2` possible comparisons between the items (with some random noise), and generate the rankings using SVC and then compare with the original ranking using spearman's correlation.

For example, the following is an input to the Algorithm:

item_1 | item_2 | comparisons result (1 means item_1 is better and vise versa)
------ | ------ | ------------------
3      | 4      | 1
2      | 5      | -1
2      | 5      | 1
5      | 9      | 1
...    | ...    | ...

And the following is the output:

item | rank
---- | ----
3    | 1
5    | 2
1    | 3
...  | ...

# Simulation Steps
In this work, we conduct a simulation by randomally generating pairwise comparisons with added noise using the following steps:

## Convert to one-hot
each pair is represented as a vector with a length equal to the number of items (N). For example:
`[1, 0, 0, 0, -1]` is a vector representing a pair `(0, 4)`. And the output of the pairwise comparison of this pair is `[1]` as we assume `0` is "better" than `4`.

## Add Noise
Randomly lie about a percentage of the pairs preference i.e. convert `[1]` to `[-1]` in some of the target class labels.

## Balance the class labels
SVCs like many classifiers like balanced class labels. We do that by randomly flipping pairs and their target classes.

## Rank and compare
Generate the Ranks and compare with the ground truth using spearman's correlation.

# Ranking Reliability
At the end, it is possible to check the expected ranking reliability by conducting further simulations and checking the number of times a ranking agrees with a certain comparison. This is important to decide how far to trust the data when evaluating systems using this data.
