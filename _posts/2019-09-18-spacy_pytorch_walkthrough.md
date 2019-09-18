---
layout: post
title: Sentiment analysis with spaCy-PyTorch Transformers
---

Trying another new thing here: There’s a really interesting example making use of the shiny new [spaCy wrapper for PyTorch transformer models](https://github.com/explosion/spacy-pytorch-transformers) that I was excited to dive into.  I figured I’m going to need to step through the code myself, so why not take a couple notes while I’m at it.  And while I’m taking a couple notes, might as well throw in a few extra words and viola, we got a blog post going.

Quick summary of what the wrapper is: It enables you to use the friendly, powerful spaCy syntax with state of the art models (e.g. BERT, XLNet) implemented in PyTorch.  A much more complete summary is [here](https://explosion.ai/blog/spacy-pytorch-transformers), but suffice to say puts a lot of new technology within reach for most anyone with some python familiarity.

This example trains a classifier on top of a pre-trained transformer model that classifies a movie review as having positive or negative sentiment.  This is an example of [transfer learning](https://bpben.github.io/2019/08/06/spacyirl_transfer/).  I’ll be stepping through the parts of the code I feel need additional explanation.

So let’s get to it!
[Code](https://github.com/explosion/spacy-pytorch-transformers/blob/master/examples/train_textcat.py)
[Colab notebook](https://colab.research.google.com/github/explosion/spacy-pytorch-transformers/blob/master/examples/Spacy_Transformers_Demo.ipynb#scrollTo=u3Qx2iVznLB-) (Note: The code I’m stepping through isn’t exactly the same as what’s in the notebook.  But this gives you an environment to play in)

```
@plac.annotations(
    model=("Model name", "positional", None, str),
    input_dir=("Optional input directory", "option", "i", Path),
    output_dir=("Optional output directory", "option", "o", Path),
    use_test=("Whether to use the actual test set", "flag", "E"),
    batch_size=("Number of docs per batch", "option", "bs", int),
    learn_rate=("Learning rate", "option", "lr", float),
    max_wpb=("Max words per sub-batch", "option", "wpb", int),
    n_texts=("Number of texts to train from", "option", "t", int),
    n_iter=("Number of training epochs", "option", "n", int),
    pos_label=("Positive label for evaluation", "option", "pl", str),
)
```
[source](https://github.com/explosion/spacy-pytorch-transformers/blob/ab132b674c5a91510eb8cc472cdbdf5877d24145/examples/train_textcat.py#L18-L29)

If my engineering experience hasn’t led me wrong, the best place to start is with the documentation.  Here we have the arguments that are being utilized by the script.  The descriptions are fairly self-explanatory, but I thought I’d dig a bit into a few of them so I (and you, fair reader) understand how to choose them.

* `use_test`: This option uses the test dataset to measure performance.  This is generally what you want to do when you’re looking at the final performance of your model (rather than running experiments).
* `batch_size`: Batch size is how much data are used with each step of each epoch.  There’s [some considerations](https://machinelearningmastery.com/difference-between-a-batch-and-an-epoch/) to take here, but these apply to essentially any gradient-based learning algorithm.
* `learn_rate`: Again, a typical parameter, which governs how much “information” each step of the training process gains from any given batch. 
* `max_wpb`: The maximum number of words in any given batch.  One of the features of the wrapper is a process for standardizing the size of inputs to the model for consistency and reduced memory footprint.  This parameter relates to that process, governing how many words are included in any particular round of updates to the model.
* `pos_label`: The positive class label.  Set this if you want to specify what is considered the “positive class”.  By default, it’s the first label in the dataset.  In this example, it’s set to “Positive”.  Careful about “first label” here, if you, for example, sort the classes “Positive” and “Negative” here, the positive class would be “negative” since, alphabetically, “n” comes before ”p”.

```
nlp = spacy.load(model)
print(nlp.pipe_names)
print(f"Loaded model '{model}'")

textcat = nlp.create_pipe(
 "pytt_textcat", config={"architecture": "softmax_last_hidden", "words_per_batch": max_wpb})
```
[source](https://github.com/explosion/spacy-pytorch-transformers/blob/ab132b674c5a91510eb8cc472cdbdf5877d24145/examples/train_textcat.py#L51-L56)

And, viola, you’ve created a state of the art NLP model architecture.  I mean, kind of.  [SpaCy’s pipeline syntax](https://spacy.io/usage/processing-pipelines/) is fairly intuitive and the fact that the new transformer wrapper makes use of it makes it that much more accessible for me.  `spaCy.load` can be used to load a model (and its pre-trained pipeline components) and `create_pipe()` can be used to add pipeline components.  

In this case, you are loading a specific PyTorch transformer model (based on the arguments passed at run time) and adding a component that enables the pipeline to use the output of the transformer in the classification task (see [TextCategorizer](https://spacy.io/api/textcategorizer) for more details).  “Pytt_textcat” is a specific architecture designed to use the output of BERT or XLNet.

Also, you’ll notice that our `max_wpb` value is used here.  As mentioned above, this will govern the size of inputs to the model during the training steps.
```
# Initialize the TextCategorizer, and create an optimizer.
optimizer = nlp.resume_training()
optimizer.alpha = 0.001
optimizer.pytt_weight_decay = 0.005
optimizer.L2 = 0.0
```
[source](https://github.com/explosion/spacy-pytorch-transformers/blob/ab132b674c5a91510eb8cc472cdbdf5877d24145/examples/train_textcat.py#L103-L106)

So now we’re moving on to the classification model training.  In order to optimize the weights on the network, we need to get the optimizer from the spaCy pipeline.  We also can set a few parameters here.  Let me go into each of them a bit

alpha: Typically this is the [learning rate](https://towardsdatascience.com/understanding-learning-rates-and-how-it-improves-performance-in-deep-learning-d0d4059c1c10) of the optimizer.  In this case, it seems to be overridden by `cyclic_triangular_rate` during the training process.  (See [here](https://github.com/explosion/spacy-pytorch-transformers/blob/ab132b674c5a91510eb8cc472cdbdf5877d24145/spacy_pytorch_transformers/wrapper.py#L132) for how that happens)
pytt_weight_decay: [A type of regularization](https://metacademy.org/graphs/concepts/weight_decay_neural_networks) for neural nets.  It ensures that weights don’t get too large.
L2: Also a type of regularization.  In this case, it’s set to zero, which means we’re relying on weight decay for regularization.

```
learn_rates = cyclic_triangular_rate(
    learn_rate / 3, learn_rate * 3, 2 * len(train_data) // batch_size
)
```
[source](https://github.com/explosion/spacy-pytorch-transformers/blob/ab132b674c5a91510eb8cc472cdbdf5877d24145/examples/train_textcat.py#L107-L109)

`cyclic_trangular_rate` is a learning rate specification that involves the learning rate “cycling” between a minimum and maximum values.  You can see the code for that [here](https://github.com/explosion/spacy-pytorch-transformers/blob/ab132b674c5a91510eb8cc472cdbdf5877d24145/spacy_pytorch_transformers/util.py#L366), but basically this snippet defines the min, max and the step-size that determines how many steps until the learning rate switches direction (i.e. increasing and decreasing).  This learning rate were originally proposed in [Smith 2017](https://arxiv.org/abs/1506.01186), but, as with all things, there’s [a Medium article](https://techburst.io/improving-the-way-we-work-with-learning-rate-5e99554f163b) for that.

```
pbar = tqdm.tqdm(total=100, leave=False)
results = []
epoch = 0
step = 0
eval_every = 100
patience = 3
while True:
# Train and evaluate
losses = Counter()
random.shuffle(train_data)
batches = minibatch(train_data, size=batch_size)
for batch in batches:
    optimizer.pytt_lr = next(learn_rates)
    texts, annotations = zip(*batch)
    nlp.update(texts, annotations, sgd=optimizer, drop=0.1, losses=losses)
    pbar.update(1)
    if step and (step % eval_every) == 0:
        pbar.close()
        with nlp.use_params(optimizer.averages):
            scores = evaluate(nlp, eval_texts, eval_cats, pos_label)
        results.append((scores["textcat_f"], step, epoch))
        print(
            "{0:.3f}\t{1:.3f}\t{2:.3f}\t{3:.3f}".format(
                losses["pytt_textcat"],
                scores["textcat_p"],
                scores["textcat_r"],
                scores["textcat_f"],
            )
        )
        pbar = tqdm.tqdm(total=eval_every, leave=False)
    step += 1
epoch += 1
# Stop if no improvement in HP.patience checkpoints
if results:
    best_score, best_step, best_epoch = max(results)
    if ((step - best_step) // eval_every) >= patience:
        break
```
[source](https://github.com/explosion/spacy-pytorch-transformers/blob/ab132b674c5a91510eb8cc472cdbdf5877d24145/examples/train_textcat.py#L113-L149)

This, I feel, is largely self-explanatory if you’ve worked with the iterative learning process before.  Essentially for each epoch, the training data is split into batches and for each batch the model is trained to predict sentiment.  The results are recorded and if, at the end of an epoch, the results do not show an improvement in performance, the training stops.  Lots of parameters to tweak here, including `eval_every`, which governs how often performance is checked, and `patience`, which governs how many steps with no improvement are tolerated before stopping.

The rest of the script uses the model to get the sentiment prediction and saves it to disk.  I find it super convenient that all of this gets wrapped in the typical spaCy syntax, which I find fairly friendly and intuitive.  This allows me to include these complex transformer models into my existing NLP pipelines without extensive tweaking.

Really impressed with what the spaCy and HuggingFace teams have come out with here.  I’m looking forward to using it more widely.  As always, let me know what you think, if you have questions, comments, complaints.  Also, if you have thoughts about this “code walkthrough” format.  I’m still figuring out how best to write these.
