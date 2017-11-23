# ranking-svc
Using SVC to rank items from pairwise comparisons. This is a demp which conducts a simulation of ranking using SVCs. the simulation assumes a list of items [1, 2, 3, ... , N] which are a ground truth ranking. We observe a partial set of the total n * ( n - 1 ) / 2 and generate the rankings using SVC and then compare with the original ranking using spearman's correlation.

# Simulation Steps

## Convert to one-hot
each pair is represented as a vector with a length equal to the number of items (N). For example:
[1, 0, 0, 0, -1] is a vector representing a pair (0, 4). And the output of the pairwise comparison of this pair is [1] as we assume 0 is "better" than 4.

## Add Noise
Randomly lie about a percentage of the pairs preference i.e. convert [1] to [-1] in some of the target class labels.

## Balance the class labels
SVCs like many classifiers like balanced class labels. We do that by randomly flipping pairs and their target classes.

## Rank and compare
Generate the Ranks and compare with the ground truth using spearman's correlation.
