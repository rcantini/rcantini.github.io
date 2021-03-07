---
title: 'Play with BERT! Text classification using Huggingface and Tensorflow'
subtitle: 'How to fine-tune a BERT classifier for detecting the sentiment of a movie review and the toxicity of a comment.'
summary: "In what follows, I'll show how to fine-tune a BERT classifier, using Huggingface and Keras+Tensorflow, for dealing with two different text classification problems. The first consists in detecting the sentiment (*negative* or *positive*) of a movie review, while the second is related to the classification of a comment based on its toxicity, expressed by one or more labels among: *toxic*, *severe toxic*, *obscene*, *threat*, *insult* and *identity hate*."
date: 2021-03-03T00:00:00Z
draft: true
math: true
disable_comments: true
markup: kramdown
lastmod: 2021-03-03T00:00:00Z
authors:
- admin
tags:
- Natural Language Processing
- Sentiment Analisysis
- Toxicity Detection
- BERT
- Deep Learning
- Keras-Tensorflow
---

In what follows, I'll show how to fine-tune a BERT classifier using the Huggingface <a href="https://huggingface.co/transformers/quicktour.html">Transformers library</a> and Keras+Tensorflow.

Two different classification problems are addressed:
- <a href="https://www.kaggle.com/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews">IMDB sentiment analysis</a>: detect the sentiment of a movie review, classifying it according to its polarity, i.e. *negative* or *positive*.
- <a href="https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/data">Toxic comment classification</a>: determine the toxicity of a Wikipedia comment, predicting a probability for each type of toxicity, i.e. *toxic*, *severe toxic*, *obscene*, *threat*, *insult* and *identity hate*.

## What is BERT?
**Bidirectional Encoder Representations from Transformers (BERT)** is a Natural Language Processing Model proposed by Google Research in 2018.
It is based on a multi-layer bidirectional Transformer, pre-trained on two unsupervised tasks using a large crossdomain corpus:
- *Masked Language Modeling (MLM)*: 15% of the words in each sequence are replaced with a `[MASK]` token. The model then attempts to predict the masked words, based on the context provided by the non-masked ones.
- *Next Sentence Prediction (NSP)*: the model receives pairs of sentences as input and learns to predict if the second sentence is the subsequent sentence in the original document.

BERT is **deeply bidirectional**, which means that it can learn the context of a word based on all the information contained in the input sequence, joinlty considering previous and subsequent tokens.
In fact, the use of MLM objective enables the representation to fuse the left and right contexts, allowing the pre-training of a deep bidirectional language representation
model.
This is a key difference comparing to previous language representation models like *OpenAI GPT*, which uses a unidirectional (left-to-right) language model, or
*ELMo*, which uses a shallow concatenation of independently trained left-to-right and right-to-left language models.
BERT outperformed many task-specific architectures, advancing the state of the art in a wide range of Natural Language Processing tasks, such as textual entailment,
text classification and question answering.

For further details, you might want to read the original <a href="https://arxiv.org/abs/1810.04805">BERT paper</a>.

## Fine-tuning
Let's now move on how to fine-tune the BERT model in order to deal with our classification tasks. Text classification can be a quite challenging task, but we can easily achieve amazing results by exploiting the effectiveness of transfer learning form pre-trained language representation models.
The first use case is related to the classification of movie reviews according to the expressed sentiment, which can be *positive* or *negative*.
The used data come from the <a href="https://www.kaggle.com/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews">IMDB dataset</a>, which contians 50000 movie reviews equally divided by polarity.
The second case study is about building a model capable of detecting different types of of toxicity like threats, obscenity, insults, and identity-based hate. The used <a href="https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/data">dataset</a> is comprised of comments from Wikipedia. This kind of models are useful for helping online discussion become more productive and respectful.
In the following, I show the Keras code for creating the models.

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
For the first case study, `n_out`=1


 I modeled this binary classification task using a classification layer with a single neuron and a sigmoid activation, which means that the model will output a single sentiment score. This is the probability that the review is positive, 
thus a value very close to \\(1\\) indicates a very positive sentence and a value near to \\(0\\) a very negative sentence, while a value close to \\(0.5\\) is related to an uncertain situation, or rather a neutral review.
As we can see, the BERT model expects three inputs:
- *Input ids*: BERT input sequence unambiguously represents both single text and text pairs. Sentences are encoded sung the WordPiece tokenizer, which recursively splits the input tokens until a word in the BERT vocabulary is detected, or the token is reduced to a single char.
 As first token, BERT uses the `CLS` special token, whose embedded representation can be used for classification purposes. Moreover, at the end of each sentence, a `SEP` token is used, which is exploited for text pairs inputs in order to differentiate between the two input sentences.
- *Input masks*: Allows the model to cleanly differentiate between the content and the padding. The mask has the same shape as the input ids, and contains 1 anywhere the the input ids is not padding.
- *Input types*: Contains 0 or 1 indicating which sentence the token is a part of. For asingle-sentence input is a vector of zeros.
This model returns two outputs which can be expoited for many dowstream tasks:
- *pooler_output*: it is the output of the BERT pooler, corresponding to the embedded representation of the CLS token further processed by a linear layer and a tanh activation. It can be used as an aggregate representation of the whole sentence. 
- *last_hidden_state*: 768-dimensional embeddings for each token in the given sentence.

The use of the first output (the pooler) is usually not a good idea, as stated in the Hugginface Transformer documentation:
> This output is usually not a good summary of the semantic content of the input, you’re often better with averaging or pooling the sequence of hidden-states for the whole input sequence.
For this reason I preferred to use a Global Average Pooling on the sequence of all hidden states, in order to get a concise representation of the whole sentence.

After the creation of the model, we can fine tune it as follows:
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
I used a number of epochs equals to 4 as a best practice and a very low learning rate. This last aspect is crucial as we only want to readapt pre-trained features to work with our downstream task, thus high gradients are not desirable at this stage. Furthermore, we are training a very large model with a relatively small amount of data and a low learning rate is a good choice for minimizing the risk of overfitting.
I used a binary cross-entropy loss as the prediction of the output class is modeled like a single Bernoulli trial, estimating the probability of a comment to be positive. Moreover I chose the Rectified version of ADAM as the optimizer for the training process.

METTERE I DUE CASI DI STUDIO INSIEME NELLA DESCRIZIONE


RectifiedADAM


<img src="emo_distr.png" style="display: block; margin-left: auto; margin-right: auto; width: 90%; height: 90%"/>


## Attention mechanism for emotion detection 
The use of **attention mechanism** in neural networks have demonstrated great success in a wide range of tasks, such as question answering, machine translations, natural language understanding and speech recognition.
The main idea behind the attention mechanism, which mimics human behaviour, is to selectively concentrate on a few relevant things, while ignoring the rest. 
There are many variations of this mechanism (*global* vs. *local*, *soft* vs. *hard*) but its main use, for enhancing LSTM models such as encoder-decoder structures (e.g. in machine translation), is to avoid the use of a **fixed context vector** as the only output of the encoder. Specifically, it is the last hidden state of the LSTM, which carries all the information extracted by the LSTM encoder. 
So, in the classical structure, all the information is compressed into the context vector, which can act as a bottleneck, while all the intermediate hidden states of the encoder are ignored. This vector is then fed to the subsequent layers, such as *LSTM decoder* or *Dense*. 
As for the subsequent steps we only depend on this kind of summarization given by the encoder, the performances can degrade as the length of the analyzed temporal sequence increases: to cope with this problem, attention mechanism is the way!

In general, according to this mechanism, every encoder hidden state, generated while processing the input sequence, is taken into account, calculating for each one of them an attention score (**energy** \\(e\\)) using an **alignment function** \\(a\\). By normalizing these scores with a softmax function, we obtain the **attention weights** (\\(\alpha\\)), which
determine the amount of attention we should pay to each hidden state in order to generate the desired output. For example, in encoder-decoder translation architectures, the attention weight \\(\alpha_{t,t'}\\) gives us a measure of the attention we should pay to the word at position \\(t'\\) while predicting the \\(t\\)-th word.
Given the attention weights for the \\(t \\)-th word, we can compute the <b>dynamic context vector</b> \\(c_t\\) as the weighted sum of the encoder hidden states: \\(c_t =\sum_{i=1}^{n}\alpha_{t,i}h_i\\). So the crucial part of the entire mechanism is to determine the attention scores, and the main implementations present today vary according to the specific alignment function they use:
- **Additive** or **concat** (*Bahdanau*): \\(e_{i,j}=v_a^Ttanh(W_as_{i-1}+U_ah_j)\\), where \\(s_{i-1}\\) is the previous decoder hidden state, \\(h_j\\) is the \\(j\\)-th encoder hidden state and \\(W_a\\), \\(U_a\\) and \\(v_a\\) are trainable matrices. We can look at the alignment model \\(a\\) as a feedforward neural network with one hidden layer.
- **Dot-product** (*Luong*): \\(e_{i,j}=s_i^T h_j\\). This model is easier than additive attention and involves no weights to train. Furthermore, the dot product can be scaled in order to improve performances, avoiding small gradients, obtaining the so-called <b>scaled dot-product attention</b>.
- Other types of attention are **location-based**, **general** and **content-based**.

For our emotion detection model I used a **Bahdanau-style global soft attention**. In particular, I adapted the formula to this classification task, where the decoder is absent. The alignment model is, like in Bahdanau, a parametrized feedforward neural network and the energies are computed as \\(e_{j}=v_a^Ttanh(U_ah_j)\\). A scaling operation is then performed for improving weights learnability. 
The context vector is then computed as the weighted sum of the encoder hidden states with the normalized energies (<i>attention weights</i>) and then concatenated to the last
encoder hidden state to improve performances. Finally, a softmax classifier is used for determining a probability distribution for the expressed emotions.


## Results

I evaluated the trained models using 20 test samples per emotion. The attention-based BLSTM achieved a 90% accuracy, while its simplified version which does not use attention achieved about 75% accuracy.

|  | Accuracy | Precision | Recall | F1-Score |
|-|-|-|-|-|
| BLSTM | 0.75 | 0.75 | 0.75 | 0.74 |
| Attention-based BLSTM | 0.90 | 0.91 | 0.90 | 0.90 |

As we can easily see, the use of the attention mechanism has led to much higher performances than a classical BSLTM. To better see the performance improvement in recognizing the different emotions, confusion matrices for both models are provided:
<img src="cf_ms.png" style="display: block; margin-left: auto; margin-right: auto; width: 100%; height: 100%"/>
We can clearly see a good improvement in recognizing every emotion, most of all for what concerns disgust, happiness and neutral classes.

Just to make it more fun, giving you some more concrete examples of the system behaviour, we can choose a test file for each emotion and take a look at what the system thinks about it. (**Click :speaker: to play the audio!**)
- [Anger :speaker:](anger.wav) --- detected emotion: **anger** (0.96 confidence)
- [Boredom :speaker:](boredom.wav) --- detected emotion: **boredom** (0.89 confidence)
- [Disgust :speaker:](disgust.wav) --- detected emotion: **disgust** (0.94 confidence)
- [Fear :speaker:](fear.wav) --- detected emotion: **fear** (0.96 confidence)
- [Happiness :speaker:](happiness.wav) --- detected emotion: **happiness** (0.88 confidence)
- [Sadness :speaker:](sadness.wav) --- detected emotion: **sadness** (0.98 confidence)
- [Neutral :speaker:](neutral.wav) --- detected emotion: **neutral** (0.90 confidence)

It's pretty cool! The model correctly classified all of the selected audio files with a high level of confidence :clap::clap:

## Visualizing emotion-based attention

Lastly, an interesting thing we can do is to take a close look at the **attention weights** \\(\alpha\\), in order to analyze how the system paid attention to the provided audio files while recognizing the different emotions. 
This degree of interpretability is an awesome property of most attention-based models.
<img src="visualize_attention.png" style="display: block; margin-left: auto; margin-right: auto; width: 90%; height: 90%"/>
The plot shows the normalized cumulative sum of the attention weights, dividing the audio files into 10 blocks (*bins*) of 0.5 seconds each. As we can see, according to the different expressed emotion, 
the system focuses on different parts of the audio. For example, it concentrates most on a small group of bins for sadness and disgust, while diluting the attention on a larger part of the audio, for boredom or happiness.
Furthermore, for anger, disgust and sadness the system pays more attention to the last bins, while for boredom it focuses on the first ones.
<hr>
You can find the full code and results on GitHub at this <a href="https://github.com/rcantini/BERT_text_classification" target="_blank">link</a>.
