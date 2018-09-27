# hcluster_sg

My clone of the sourceforge subdirectory for `hcluster_sg`, Heng Li's tool for hierarchical clustering.

I am **not** maintaining this software (but [@douglasgscofield](https://github.com/douglasgscofield/hcluster) is).
I made this repo after I realised that @douglasgscofield missed some of the historical commmits when the tool was still internally called `gcluster`, because I wanted to use GitHub releases to tag the various versions, and link Heng Li's commits to his GitHub account.

*Note* that Heng Li's version 0.5.1 does not compile, and like @douglasgscofield I had to make a couple of minor changes in the code.

# Documentation

> This is some documentation I have found on the old TreeFam website, which
> is not available anywhere else.

`hcluster_sg` performs hierarchical clustering under mean distance. It
reads an input file that describes the similarity between two sequences,
and groups two nearest nodes at each step. When two nodes are joined, the
distance between the joined node and all the other nodes are updated by
mean distance. This procedure is iterated until one of the three rules is
met:

* Do not merge cluster A and B if the total number of edges between A and B
  is smaller than `|A|*|B|/3`, where `|A|` and `|B|` are the sizes of A and
  B, respectively. This rule guarantees each cluster is compact.
* Do not join A to any other cluster if `|A| < 500`. This rule avoids huge
  clusters which may cause computational burden for multiple alignment and
  tree building as well.
* Do not join A and B if both A and B contain plant genes or both A and B
  contain Fungi genes. This rule tries to find animal gene families.
  TreeFam clustering is done with outgroups.
  **NOTE**: this is the _category_ parameter.

`hcluster_sg` also introduces an additional edge breaking rule: removes an
edge between cluster A and B if the number of edges between A and B is
smaller than `|A|*|B|/10`. This heuristic rule removes weak relations which
are quite unlikely to be joined at a later step.
