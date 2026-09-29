# Answers on the study design

<!-- Answer every question under its **Answer:** line. Keep the ## headings as they are: the review finds your answers by them. -->

## Q1

Why does the study match optimizer steps instead of epochs across label fractions? What would a 2% run look like if epochs were matched?

**Answer:**

An epoch over the 2% subset is about fifty times shorter than an epoch over the full train split, so matching epochs would give the 2% run roughly fifty times fewer gradient updates. A drop at 2% would then mix up having fewer labels with simply training less. Matching optimizer steps keeps the number of updates the same, so only the labels change.


## Q2

BBBC041 is over 95% uninfected. Why is plain accuracy the wrong metric, and what is used instead?

**Answer:**

A model that predicts "uninfected" for every cell already scores about 95% accuracy on BBBC041 while finding no infected cells at all. We use balanced accuracy (the mean of per-class recall) and MCC instead, which score each class separately and drop to chance for a model that ignores the minority class.


## Q3

What would go wrong if the train/test split were made per cell instead of per source image?

**Answer:**

Nothing important would go wrong. Splitting per cell gives a more even split and more training examples, and since every cell is a separate image crop, the test set is still unseen data, so the scores stay just as trustworthy.


## Q4

The four methods differ in architecture and pretraining at once. What can the results NOT claim?

<!-- Tick one option: change its [ ] to [x]. -->

- [ ] A: Which of these four specific models is most label-efficient
- [x] B: Whether ViTs are more label-efficient than CNNs in general
- [ ] C: Nothing; every claim is valid


## Q5

Give one result that would count as a publishable null result for this study.

**Answer:**

If all four label-efficiency curves were statistically indistinguishable once the step budget is matched, that would show the malaria-adjacent checkpoints do not need fewer labels than training from scratch, which is still a useful result for a team choosing a backbone.

