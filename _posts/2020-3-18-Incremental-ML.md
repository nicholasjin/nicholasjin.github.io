---
title: 'Incremental Machine Learning'
date: 2020-03-18
permalink: /posts/incremental/
tags:
  - machine learning
  - online learning
---
Welcome back to Esoteria! Today, we're going to talk about a paradigm of machine learning called _online machine learning_. We will compare and contrast this with _batch learning_, the paradigm under which introductory machine learning is usually taught, and demonstrate how to use it in a practical application via the library `creme`.

Along the way, we demonstrate that one of the results presented in [this paper](https://www.ijcai.org/Proceedings/11/Papers/254.pdf) is _too good_. The authors claimed ROCAUC scores of .982 and .996 classifying the `HTTP` dataset with Half-Space Trees. Using two different libraries, we demonstrate that this result is only possible due to *data leakage*: by improperly preprocessing the dataset, they exposed future information to the model during its training.

# Batch learning
If we have a passing familiarity with machine learning, then batch learning is an old friend. Batch learning follows a familiar sequence of steps:
1. Load a dataset into memory
2. Train a model on the entirety of that dataset
3. Use the trained model to predict on unseen data

Batch models are simple, elegant, and get to learn on all the data at once. They are 'default' for a reason! That said, batch learning has downsides. If we want to update our model, usually we have to retrain on the entire dataset, and this is computationally expensive if repeated often. Often, the full dataset cannot fit into memory ― and so we can resort to tricks to try and do better (e.g. sparse matrices, out-of-core algorithms), but these workarounds have limits.

Batch models are also rigid, in the sense that they have fixed parameters. A batch linear regression has a set number of $\beta_i$'s, and those simply cannot change. If the data ends up having more features at a later date, then you're out of luck; you'll need to figure out how you want to process the new data, and then _retrain your model_. The rigidity of batch model parameters can lead to the accumulation of _technical debt_, as you have to jump through more and more hoops to make new data fit your old model (alternatively, you may need to update a model many times to incorporate new data).

More generally, batch learning can struggle to deal with content drift ― the idea that data and relationships in the data can change over time.

# Online Machine Learning
Online machine learning attempts to address all of these deficiencies by predicting and learning on data one observation at a time. In batch learning, we separated data into a *training set* and a *testing set*. In online learning, there is no such distinction; each new datum is a *test* example, and after we've made a prediction we can then add it to our model as a *training* example.

In a batch setting, we made the implicit assumption that our data is sampled i.i.d from the same distribution. In online learning, we make no such assumptions. In particular, the input can be allowed to be adversarial (e.g. spam filtering).  

For a more formal introduction to Online Learning, see [Chapter 21 of *Understanding Machine Learning: From Theory to Algorithms*](https://www.cse.huji.ac.il/~shais/UnderstandingMachineLearning/). For semi-obvious reasons, trying to search for "online learning" can return a large number of fairly useless results.
# `Creme`
`creme` is a library for online machine learning, styled after `sklearn`. It supports most elementary machine learning models, preprocessing, pipelines, and provides wrappers for classes not yet implemented. It is still undergoing rapid development.

One of the things I liked most about `creme` was the syntax used to construct pipelines.

```python
ohe_list = [preprocessing.OneHotEncoder(col) for col in cols_string]
string_processor = compose.TransformerUnion(ohe_list)

num_processor = compose.Blacklister(*cols_string)|preprocessing.StandardScaler()

model = string_processor + num_processor
model |= linear_model.LogisticRegression()
model.draw()
```

![](/images/creme-pipeline.svg)

`creme` overloads the pipe operator \| to mean what it would in a unix context. In the example above, the `flag`, `protocol_type`, and `service` columns are string columns, and so need to be one hot encoded; all the other columns are numeric, and so need to be scaled. `model.draw()` allows you to inspect the pipeline you've constructed to make sure it is correct.

In [this notebook](https://github.com/nicholasjin/incremental_ids/blob/master/KDD/04_KDD_incremental_logreg_no_shuffle.ipynb), we demonstrate how to build an incremental logistic regression using `creme`. We achieve an ROCAUC of 0.995 on the KDD99 dataset. Note that `creme` is *fast*. Creme predicts and trains on half a million entries in 3.5 minutes on my machine. A comparable logistic regression using `sklearn` took my machine 50 minutes.

# Anomaly detection with Half-Space Trees
Half-Space Trees are a fast, streaming one-class anomaly detector. In short, HSTs are an ensemble of trees which recursively partition feature space, assigning a *mass profile* to score each observation. We won't talk too much about the technical details of this approach ― interested readers can read the original paper [here](https://www.ijcai.org/Proceedings/11/Papers/254.pdf) \( and [this paper](https://zhougt.github.io/research/mass_kdd10.pdf) describes their _mass estimation_ method). 

The authors reported ROCAUC scores of .982 and .996 on the HTTP dataset using HSTs. We benchmarked HSTs using their implementations in both `creme` [(notebook)](https://github.com/nicholasjin/incremental_ids/blob/master/KDD/07_creme044_benchmark.ipynb) and `scikit-multiflow` [(notebook)](https://github.com/nicholasjin/incremental_ids/blob/master/KDD/08_skmultiflow_benchmark.ipynb). It is worth noting that `scikit-multiflow` does not implement a streaming scaler, so I do not know how well their implementation performs on other datasets.

We show that the only way to for an HST anomaly detector to perform remotely well on the `HTTP` dataset is to prescale and shuffle the dataset. We discuss below why both operations are highly questionable.

## Prescaling
Prescaling the dataset is an example of *data leakage*: it invalidates the entire paradigm of online learning, since it involves taking a second pass over the data. If our algorithm is learning on data that has been rescaled using future data, then it is learning on future data. So no data will be entirely "new"; some of its information has already been seen by the model.

## Shuffling
If a dataset has particular temporal qualities, then shuffling the dataset is invalid. An obvious example is in time series analysis, where shuffling your data destroys temporal relationships. The `HTTP` dataset is another dataset that should not be shuffled, as it has a particular temporal structure: it is majority background traffic, punctuated by infrequent bursts of malicious activity. Since HSTs depend on the most recent observations to score anomalies, large bursts of similar-looking malicious traffic can be difficult to distinguish from shifting background. Shuffling `HTTP` destroys its fundamental character, and obscures the difficulty HSTs encounter attempting to classify it.

# Conclusion
Hopefully you've enjoyed this little introduction to online learning. I've re-linked some resources to some textbooks and python libraries should you feel the desire to explore.
# More resources
The documentation for `creme` can be found [here](https://creme-ml.github.io/).

The documentation for `scikit-multiflow` can be found [here](https://scikit-multiflow.github.io/scikit-multiflow/index.html).

A more rigorous introduction to online learning can be found on chapter 21 of [*Understanding Machine Learning: From Theory to Algorithms*](https://www.cse.huji.ac.il/~shais/UnderstandingMachineLearning/)

[Vowpal Wabbit](https://vowpalwabbit.org/index.html) is another library for online learning. I have not spent any time with it, but it is supposed to be quite powerful!
