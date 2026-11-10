---
id: loss-functions
type: concept
title: "Loss Functions"
aliases: ["Training loss", "Objective function"]
domains: ["foundations", "time-series", "nlp", "computer-vision"]
---

# Loss Functions

## What they are and why they matter

A loss assigns a numerical cost to a prediction. Training minimizes an objective built from these costs, sometimes with additional penalties. The choice encodes what mistakes the model is encouraged to avoid.

A training loss and an operational metric need not be the same. For example, token cross-entropy supports gradient-based training, while an application may care about task success or latency.

## Mechanism

For scalar regression, mean squared error over $N$ examples is:

$$
L_{\mathrm{MSE}}=\frac1N\sum_{n=1}^N(\hat y_n-y_n)^2.
$$

For categorical prediction with target distribution $y$ and predicted distribution $p$:

$$
L_{\mathrm{CE}}=-\sum_{i=1}^K y_i\log p_i.
$$

With a one-hot target, only the correct class contributes. Natural logarithms make the unit a nat. For independent binary labels, binary cross-entropy applies separately to each label; the outputs do not need to sum to one.

If $p=\operatorname{softmax}(z)$, the gradient of categorical cross-entropy with respect to logits is $p-y$. This compact result is one reason to combine the operations in implementation.

## Worked example

A regression prediction of $3$ for target $5$ has squared error $4$ and derivative $2(3-5)=-4$ with respect to the prediction.

For categorical predictions $[0.2,0.8]$ and a correct second class, the loss is $-\log0.8\approx0.223$. If the correct class is the first, it is approximately $1.609$.

## Engineering implications

- Match output semantics to the loss. Do not treat multiclass and multilabel classification as interchangeable.
- Check reduction: summing rather than averaging changes gradient scale with batch size or sequence length.
- Exclude padding from sequence losses and average over valid positions deliberately.
- Fit preprocessing on training data and evaluate on held-out examples. A lower training loss alone does not demonstrate useful generalization.
- For time series, preserve chronology in evaluation. Leakage can make a poor model look effective regardless of its loss function.

## Graph connections

- **uses:** [Softmax](softmax.md) — in categorical cross-entropy.
- **used_by:** [Gradient descent](gradient-descent.md), [Backpropagation](backpropagation.md), [Regularization](regularization.md)
- **related_to:** [MLP](multi-layer-perceptron.md)
- **supported_by:** [Backpropagation](../papers/rumelhart-1986-backpropagation.md) — a foundational squared-error treatment.
- **supported_by:** [Attention Is All You Need](../papers/vaswani-2017-attention.md) — a milestone sequence-modeling application; these papers did not originate all losses above.
