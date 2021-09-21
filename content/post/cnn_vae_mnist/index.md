---
title: "Let's play with MNIST! Generate digits with Convolutional Variational Autoencoders"
subtitle: 'How to develop and deploy a web application for drawing numbers that leverages a CNN-based variational autoencoder trained on the MNIST dataset of handwritten digits.'
summary: "This post is dedicated to the development of a Flask web application capable of drawing digits through the use of a generative model. This model is obtained by training a convolutional variational autoencoder on the MNIST dataset of handwritten digits using Keras+Tensorflow."
date: 2021-08-15T00:00:00Z
draft: false
math: true
disable_comments: true
markup: kramdown
lastmod: 2021-08-15T00:00:00Z
authors:
- admin
tags:
- Computer Vision
- Generative Models
- MNIST
- Deep Learning
- Keras-Tensorflow
- Flask
---

In this post I'll introduce variational autoencoders, showing how they can be applied to the generation of new synthetic images depicting handwritten digits.
I'll describe how to setup and train a CNN-based variational autoencoder using Keras with Tensorflow backend, embedding this generative model within a Flask web application.

## Classical autoencoder
An **autoencoder** is a particular model that allows to efficiently encode a set of data of interest in an unsupervised manner.
The purpose of this system is to learn a representation of a given input, called encoding, in order to reduce its dimensionality, often high, as in a sort of compression.
In particular, an autoencoder consists of a pair of interconnected neural networks, known as *encoder* and *decoder*, which are often multilevel perceptrons or convolutional neural networks (CNNs).
The encoder receives an input instance and derives a dense representation in a space with a smaller dimensionality, called *latent space*;
the decoder, afterwards, is able to reconstruct the original input starting from its compressed version.
The training phase involves both networks at the same time, as the encoder learns how to significantly map the input instances in the latent space, while the decoder improves its ability to recompose the output starting from the encoded representation in the space of the latent variables, all aiming to minimize the reconstruction error.
Despite the clear utility of classical autoencoders in tasks like image segmentation, neural inpainting and denoising, they suffer in the context of data generation as the latent space, where the codified vectors lie, is not a continuous space.
This issue hinders the generative power of these systems as well as the possibility of interpolation, as they can not correctly manage points related to encodings coming from unknown latent space region, which leads to the reconstruction of an unrealistic output.

## Variational autoencoders
In order to overcome the problems that the GAN and classic autoencoders suffer, a different class of generative models can be used, the so called **Variational Autoencoders** (VAE), based on Bayesian inference.
These models aim to model the probability distribution underlying the data, in order to obtain new instances by sampling this distribution.
The main characteristic of a variational autoencoder, which distinguishes it from a standard autoencoder, is the continuity of the space of its latent variables:
in fact, the purpose of such systems is to represent any latent attribute in probabilistic terms, using a distribution instead of a single point value.
Given a certain observation \\( x \\), the purpose of these systems is to infer the characteristics of one or more latent variables \\( z \\) that generate \\( x \\); this is equivalent to compute the conditional probability:

$$
p\left( {z|x} \right) = \frac{{p\left( {x|z} \right)p\left( z \right)}}{{p\left( x \right)}}\end{math}
$$

The probability expressed in Bayesian terms, is however too hard to compute, since the calculation of the evidence, involves a marginalization leading to an intractable distribution:

$$
p\left( x \right) = \int {p\left( {x|z} \right)p\left( z \right)dz}\end{math}
$$

To overcome this problem, Variational Inference can be used, since it allows the estimation of this value by approximating the distribution through optimization techniques.
In particular, the \\( p\left( {z|x} \right) \\) distribution can be approximated with a tractable one, \\( q\left( {z|x} \right) \\), whose parameters are estimated to make the two distributions as similar as possible.
The dissimilarity between the two distributions is measured by the Kullback-Leibler divergence.
Starting from this the loss function for a VAE can be derived and written as follows in terms of minimization:
$$
\min{{\cal L}\left( {x,\hat x} \right) + \sum\limits_j {KL\left( {{q_j}\left( {z|x} \right)||p\left( z \right)} \right)}}
$$

where the first term penalizes the reconstruction error, while the second estimates how much the learned distribution is similar to the original one, which is assumed to be approximable with a Gaussian of zero mean and unit variance, for each latent space dimension.
Intuitively, this formulation forces the encoder to distribute all the encodings around the origin of the latent space, differentiating them according to the salient characteristics of each type of input, a process that leads to the formation of a clustering structure.
Both terms are necessary:
- The *reconstruction loss* force the reconstructed images to be as similar as possible to the original one, getting the VAE to discern the characteristics that distinguish each type of image, a process that induces the formation of a cluster for each type.
- The *KL divergence* works as a regularizer and forces the codings to be sufficiently close to each other, to guarantee the possibility of interpolate encodings lying in different clusters, compacting the clusters within the latent space.
This formulation leads to the generation of instances whose features are the result of a fuzzy combination of latent features of different types, which can be well interpreted by the decoder.


STRUTTURA, REPARAMETRIZZAZIONE, IMPLEMENTAZIONE IN KERAS, APP FLASK




For further details, you might want to read the original <a href="https://arxiv.org/abs/1810.04805">BERT paper</a>.

## Fine-tuning
Let's now move on how to fine-tune the BERT model in order to deal with our classification tasks. Text classification can be a quite challenging task, but we can easily achieve amazing results by exploiting the effectiveness of transfer learning form pre-trained language representation models.
The first use case is related to the classification of movie reviews according to the expressed sentiment, which can be *positive* or *negative*.
The used data come from the <a href="https://www.kaggle.com/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews">IMDB dataset</a>, which contians 50000 movie reviews equally divided by polarity.
The second case study is about building a model capable of detecting different types of toxicity like threats, obscenity, insults, and identity-based hate. The used <a href="https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/data">dataset</a> is comprised of a large number of comments from Wikipedia. Toxicity detection models are useful for helping online discussion become more productive and respectful.

In the following, I show my Keras code for creating the models.

```python
def create_model(n_out):
    input_ids = layers.Input(shape=(MAX_SEQ_LEN,), dtype=tf.int32, name='input_ids')
    input_type = layers.Input(shape=(MAX_SEQ_LEN,), dtype=tf.int32, name='token_type_ids')
    input_mask = layers.Input(shape=(MAX_SEQ_LEN,), dtype=tf.int32, name='attention_mask')
    inputs = [input_ids, input_type, input_mask]
    bert = TFBertModel.from_pretrained(BERT_NAME)
    bert_outputs = bert(inputs)
    last_hidden_states = bert_outputs.last_hidden_state
    avg = layers.GlobalAveragePooling1D()(last_hidden_states)
    output = layers.Dense(n_out, activation="sigmoid")(avg)
    model = keras.Model(inputs=inputs, outputs=output)
    model.summary()
    return model
```
The only difference between the two models is the number of neurons in the output layer, i.e. the number of independent classes, determined by the `n_out` parameter.
For the first case study, `n_out` is equal to \\(1\\), as we are coping with a binary classification task that involves the calculation of a single sentiment score. This is the probability that the review is positive, 
thus a value close to \\(1\\) indicates a very positive sentence, a value near to \\(0\\) a very negative sentence and a value close to \\(0.5\\) is related to an uncertain situation, or rather a neutral review.
For the second case study, `n_out` is equal to \\(6\\), as we are coping with a multi-label classification with six possible types of toxicity. This means that the model treats each toxicity type as a separate class, computing an independent probability for each one of them through a Bernuolli trial.

As we can see, the BERT model expects three inputs:
- **Input ids**: BERT input sequence unambiguously represents both single text and text pairs. Sentences are encoded using the WordPiece tokenizer, which recursively splits the input tokens until a word in the BERT vocabulary is detected, or the token is reduced to a single char.
 As first token, BERT uses the `CLS` special token, whose embedded representation can be used for classification purposes. Moreover, at the end of each sentence, a `SEP` token is used, which is exploited for differentiating between the two input sentences in the case of text pairs.
- **Input mask**: Allows the model to cleanly differentiate between the content and the padding. The mask has the same shape as the input ids, and contains 1 anywhere the the input ids is not padding.
- **Input types**: Contains 0 or 1 indicating which sentence the token is a part of. For a single-sentence input, it is a vector of zeros.

Huggingface model returns two outputs which can be expoited for dowstream tasks:
- **pooler_output**: it is the output of the BERT pooler, corresponding to the embedded representation of the `CLS` token further processed by a linear layer and a *tanh* activation. It can be used as an aggregate representation of the whole sentence. 
- **last_hidden_state**: 768-dimensional embeddings for each token in the given sentence.

The use of the first output (coming from the pooler) is usually not a good idea, as stated in the Hugginface Transformer documentation:
> This output is usually not a good summary of the semantic content of the input, you’re often better with averaging or pooling the sequence of hidden-states for the whole input sequence.

For this reason I preferred to use a *Global Average Pooling* on the sequence of all hidden states, in order to get a concise representation of the whole sentence. Another thing that usually works is to directly take the embedded representation of the `CLS` token, before it is fed to the BERT pooler.

After the creation of the model, we can fine-tune it as follows:
```python
def fine_tune(model, X_train, x_val, y_train, y_val):
    max_epochs = 4
    batch_size = 32
    opt = tfa.optimizers.RectifiedAdam(learning_rate=3e-5)
    loss = keras.losses.BinaryCrossentropy()
    best_weights_file = "weights.h5"
    m_ckpt = ModelCheckpoint(best_weights_file, monitor='val_auc', mode='max', verbose=2,
                             save_weights_only=True, save_best_only=True)
    model.compile(loss=loss, optimizer=opt, metrics=[keras.metrics.AUC(multi_label=True, curve="ROC"),
                                                     keras.metrics.BinaryAccuracy()])
    model.fit(
        X_train, y_train,
        validation_data=(x_val, y_val),
        epochs=max_epochs,
        batch_size=batch_size,
        callbacks=[m_ckpt],
        verbose=2
    )
```
I trained the model for \\(4\\) epochs using a very low learning rate (\\(3e^{-5}\\)). This last aspect is crucial as we only want to readapt the pre-trained features to work with our downstream task, thus large weight updates are not desirable at this stage. 
Furthermore, we are training a very large model with a relatively small amount of data and a low learning rate is a good choice for minimizing the risk of overfitting.
I used a *binary cross-entropy* loss as the prediction of each of the `n_out` output classes is modeled like a single Bernoulli trial, estimating the probability through a sigmoid activation. Moreover I chose the *Rectified version of ADAM (RAdam)* as the optimizer for the training process. 
**RAdam** is a variant of the Adam optimizer which rectifies the variance and generalization issues apparent in other adaptive learning rate optimizers. The main idea behind this variation is to apply a warm-up with a low initial learning rate, turning also off the momentum term for the first few sets of input training batches.
Lastly, I used the *area under the Receiver operating characteristic curve (ROC AUC)*, and *binary accuracy* as the main metrics for validation and testing.

## Training epochs
In the following, the results of the 4 training epochs of both models are shown:
<p style="text-align: center"><b>Sentiment analysis, IMDB movie reviews</b></p> 
<img src="training_sent.png" style="display: block; margin-left: auto; margin-right: auto; width: 100%; height: 100%"/>
<p style="text-align: center"><b>Toxicity detection, Wikipedia toxic comments</b></p> 
<img src="training_tox.png" style="display: block; margin-left: auto; margin-right: auto; width: 100%; height: 100%"/>

## Results

I evaluated the trained models using \\(1024\\) test samples, achieving the following results:

|  | Test BCE loss | Binary accuracy |     ROC AUC     |
|:-:|:-:|:-:|:-:|
| Sentiment classification | 0.26 | 0.88 | 0.95 |
| Toxicity classification | 0.05 | 0.98 | 0.94 |

As we can see, the easy use of a fine-tuned BERT classifier led us to achieve very promising results, confirming the effectiveness of transfer learning from language representation models pre-trained on a large crossdomain corpus. 
To better analyze the performance of the trained classifiers, *ROC curves* for both models are provided:
<img src="roc_auc.png" style="display: block; margin-left: auto; margin-right: auto; width: 100%; height: 100%"/>
We can clearly see the high confidence of both models, especially for what concerns the toxicity classifier which achieved a micro-average ROC AUC of \\(0.98\\).

Just to make it more fun, I wrote some sentences to further test the performance of both models.
<p style="text-align: center"><b>Sentiment analysis, IMDB movie reviews</b></p> 
<img src="pred_sent.png" style="display: block; margin-left: auto; margin-right: auto; width: 90%; height: 90%"/>
<p style="text-align: center"><b>Toxicity detection, Wikipedia toxic comments</b></p> 
<img src="pred_tox.png" style="display: block; margin-left: auto; margin-right: auto; width: 90%; height: 90%"/>

Good job! :clap::clap: The first model correctly classified the polarity of all movie reviews, even in the presence of sarcasm (look at the last review). 

On the other hand, the second model detected correctly the presence of toxicity in Wikipedia comments or its absence (last comment). It also determined the right types of toxicity, like obscene, toxic and insult for the first and the third comments, or threat for the second one (yes, that's a Liam Neeson quote...I couldn't resist! :laughing:).

## Application

In the following the app:

<iframe src="https://play-with-mnist.herokuapp.com/" width="100%" height="708px"></iframe>

<hr>
You can find the full code and results on GitHub at this <a href="https://github.com/rcantini/BERT_text_classification" target="_blank">link</a>.