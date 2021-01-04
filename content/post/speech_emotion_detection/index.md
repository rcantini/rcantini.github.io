---
title: 'Emotion detection from speech using Bi-directional LSTM networks and attention mechanism in Keras'
subtitle: 'How to exploit attention mechanism in LSTM networks for realizing a sentiment analysis application that can distinguish among seven different emotional states: *anger*, *boredom*, *disgust*, *fear*, *happiness*, *sadness* and *neutral*'
summary: "This post is dedicated to the development of an artificial intelligence application capable of identifying the emotions expressed through the voice in spoken language. The classification model focuses on seven different emotions (*anger*, *boredom*, *disgust*, *fear*, *happiness*, *sadness*, *neutral*) and is enhanced with the attention mechanism."
date: 2020-12-29T00:00:00Z
draft: true
math: true
disable_comments: true
markup: kramdown
lastmod: 2020-12-29T00:00:00Z
authors:
- admin
tags:
- Emotion detection
- Sentiment Analisysis
- LSTM
- Attention
- Audio analysis
- Deep Learning
- Keras-Tensorflow
---

This post is dedicated to the development of an artificial intelligence application capable of identifying the emotions expressed through the voice in spoken language.
The classification system focuses on seven different emotions (*anger*, *boredom*, *disgust*, *fear*, *happiness*, *sadness*, *neutral*) and exploits an attention-based Long Short-Term Memory (LSTM) neural network, a state-of-art deep learning model for the analysis of sequential data, widely used in the field of Natural Language Processing (NLP).

## Long Short-Term Memory Networks
The main idea behind this kind of deep learning model is simple but powerful and is inspired by the way reasoning occurs in the human brain. In particular, humans don't start thinking from scratch every time, but they use memory in order to interpret better a given information contextualizing it based on past information.
This kind of persistency, which is absent in traditional feed-forward neural networks, is realized with **Recurrent Neual Networks** (RNN).
These networks are able to use past information thanks to their loop structure, which can be be better represented by unrolling the network through time.
<img src="unrolled.png" style="display: block; margin-left: auto; margin-right: auto; width: 90%; height: 90%"/>
Persistency of information is achieved passing the current *hidden state* to the next step of the sequence. So the hidden state at each time step carries information about what the neural network has seen so far, acting like a memory element.
At the time \\(t\\), the hidden state \\(h_t\\) is computed as the concatenation of the previous hidden state \\(h_{t-1}\\) and the current element of the input sequence \\(x_t\\), which undergoes a non-linear transformation through the tanh activation.
<img src="rnn.gif" style="display: block; margin-left: auto; margin-right: auto; margin-top: -10px; width: 100%; height: 100%"/>

The problem of these kind of networks is that information cannot be carried effectively if the time sequence is too long, which means that we could lose important connections if the distance between useful information and the instant in which it is needed is very large.
For dealing with long short-term dependencies, **Long Short-Term Memory** networks (LSTM) have been proposed, whose architecture is showed below.
<img src="LSTM.png" style="display: block; margin-left: auto; margin-right: auto; width: 90%; height: 90%"/>
The key element in LSTM networks is the *cell state*, which acts like memory element, undergoing only a few transformations along the entire chain. In particular, the flow of information is regulated by three structures called gates.
- *Forget gate*: determines to what extent the components of the cell state must be maintained, by calculating a score using the sigmoid function.
$$
f_{t}= \sigma (W_f \cdot [h_{t-1}, x_t] + b_f)
$$
- *Input gate*: determines what new information to store in the cell state. In particular, a sigmoid layer chooses which state values ​​should be updated, while a tanh layer determines the new candidate values.
$$
i_{t}= \sigma (W_i \cdot [h_{t-1}, x_t] + b_i)
$$
$$
\tilde{C}_t = tanh(W_c \cdot [h_{t-1}, x_t] + b_i)
$$
At this time the cell state can be updated as: \\(C_t =f_t*C_{t-1}+i_t*\tilde{C}_t\\).
- *Forget gate*: determines the final output of the module as a filtered version of the updated cell state:
$$
o_{t}= \sigma (W_o \cdot [h_{t-1}, x_t] + b_o)
$$
$$
h_t = o_t*tanh(C_t)
$$


## Emotion detection
Let's now move on how to use LSTM Neural Networks in Keras in order to build our emotion detection application. Our dataset is the <a href="https://www.kaggle.com/piyushagni5/berlin-database-of-emotional-speech-emodb">Berlin Dataset of Emotional Speech (EMO-DB)</a>.
For its construction 10 actors have been used, who were asked to read 10 portions of different text simulating seven different emotions: anger, boredom, disgust, anxiety, fear,
happiness, sadness and a neutral version that does not belong to any emotional state. The recordings were made at a frequency of 48kHz, subsampled to 16kHz, inside anechoic chambers provided by the University's Department of Technical Acoustics
of Berlin which are designed to minimize the distorting effects of noise.
Classifying these recordings according to the expressed emotion is a quite challenging task, as the input data must be represented in an effective way and the patterns to be learned are quite complex.

## Feature extraction
Features have been extracted from wav format audio files by exploiting **Librosa**, a python package for music and audio analysis. In particular, I used the following 46 features:
- *Spectral centroid*: indicates where the centre of mass for a sound is located and is calculated as the weighted mean of the sound frequencies.
- *Spectral contrast*: estimates the energy contrast by comparing the peak energy to the valley energy.
- *Spectral bandwidth*: is the wavelength interval in which a spectral quantity is not less than half its maximum value.
- *Spectral rolloff*: represents the frequency below which a specified percentage of the total spectral energy lies.
- *Zero crossing rate*: is the rate at which the signal changes from positive to negative or back.
- *Root Mean Square*: describes the average signal amplitude.
- *Mel frequency cepstral coefficients (MFCCs)*: a small set of features (20 coefficients) which model the characteristics of the human voice, concisely describing the overall shape of the spectral envelope.
- *MFCC's first order derivatives*: 20 coefficients which capture the ways in which the MFCCs of the audio signal vary over time.
I used a frame length \\(l=512\\) and imposed a maximum duration of \\(d=5\\) seconds. So, as we have a frequency \\(f=16 kHz\\) for audio signals, we will have a number of frames \\(N = ceil(f*d/l) = 157\\)
Computing the above 46 features for each of the 157 frames and each of the 535 audio files, we will end up with a \\(3D\\) input datased with shape \\(535\times 157\times 46\\), which is very suitable to be analyzed with an LSTM model.
In fact, we can look at each file in our dataset as a time sequence of 157 frames, each one containing its descriptive features.

## Class balancing
The dataset is composed by 535 audio files, whose emotion distribution is showed below:
<img src="emo_distr.png" style="display: block; margin-left: auto; margin-right: auto; width: 70%; height: 70%"/>
As we can see, training samples are quite unbalanced, which can cause problems in recognizing less represented emotions, such as disgust or sadness.
To cope with this issue I used a class balancing strategy called **Synthetic Minority Over-sampling Technique** (SMOTE). it is an oversampling technique, which consists in increasing the number of samples relating to the less represented classes.
In particular, new synthetic examples are created through interpolation techniques in order to obtain the same number of samples per class. After class balancing, the dataset contains 749 example from which 20 non-synthetic samples per class are selected as our test set.
Is crucial here to select non-synthetic test samples for measuring fairly the performance of the classification model.


## Attention mechanism for emotion detection 
The use of attention mechanism in neural networks have widely demonstrated success in a wide range of tasks such as question answering, machine translations, natural language understanding and speech recognition.
The main idea behind the attention mechanism, which mimics human behaviour, is to selectively concentrate on a few relevant things, while ignoring the rest. 


The Keras implementation of the model is showed below:
```python
def create_model(units=256):
    input = keras.Input(shape=(pre_proc.N_FRAMES, pre_proc.N_FEATURES))
        states, forward_h, _, backward_h, _ = layers.Bidirectional(
            layers.LSTM(units, return_sequences=True, return_state=True)
        )(input)
        last_state = layers.Concatenate()([forward_h, backward_h])
        tanh = layers.TimeDistributed(layers.Activation("tanh"))(states)
        scores = layers.TimeDistributed(layers.Dense(1, activation='linear', use_bias=False))(tanh)
        f_scores = layers.Flatten()(scores)
        a = layers.Softmax()(f_scores)
        r = layers.Dot(axes=1)([states, a])
        vec = layers.Concatenate()([r, last_state])
    elif MODEL == "BLSTM":
        vec = layers.Bidirectional(layers.LSTM(units, return_sequences=False))(input)
    else:
        raise Exception("Unknown model architecture!")
    pred = layers.Dense(pre_proc.N_EMOTIONS, activation="softmax")(vec)
    model = keras.Model(inputs=[input], outputs=[pred])
    print(str(model.summary()))
    return model
```

## Training the model with real time data augmentation
Now our model is ready for the training step.
As the amount of images available for training the model is small, we can use an ImageDataGenerator in order to obtain some additional training samples:
```python
datagenTrain = ImageDataGenerator(
    featurewise_center=True,
    featurewise_std_normalization=True,
    rotation_range=20,
    width_shift_range=0.2,
    height_shift_range=0.2,
    horizontal_flip=True)
datagenTrain.fit(xTrain)
```
Now we can use our generator while training the model, obtaining real time **data augmentation**:
```python
# compile model
model.compile(loss='categorical_crossentropy', optimizer="adam", metrics=['accuracy'])
# set callbacks for early stopping
es = EarlyStopping(monitor='val_loss', mode='min', verbose=1, patience=5)
best_weights_file = "weights.h5"
mc = ModelCheckpoint(best_weights_file, monitor='val_loss', mode='min', verbose=2,
                     save_best_only=True)
# train model testing it on each epoch with real time data augmentation
history = model.fit(datagenTrain.flow(xTrain, y_train_cat, save_to_dir= "data_aug", batch_size=32), validation_data=(xTest, y_test_cat),
                    batch_size=32, callbacks= [es, mc], epochs=50, verbose=2)
```
An example of what images our generator produces, using 20° rotation, shift and horizontal flip, is showed below:
<img src="data_aug.png" style="display: block; margin-left: auto; margin-right: auto; width: 100%; height: 100%"/>
The model has been trained using the *categorical crossentropy* loss function and the *Adam* optimizer. Furthermore two callback functions have been used in oder to avoid overfitting: *EarlyStopping*, which monitors the loss on validation set, and *ModelCheckpoint* for storing the best model.

## Fine tuning
An additional step for further improving performances is **fine tuning**. It consists in re-training the entire model obtained above in order to incrementally adapt the pretrained features to our specific dataset.
Specifically, fine tuning can be obtained as follows:
- Load the best model achieved in the previous training step
- Un-freeze the pretrained layers. I've choosen to make the entire model trainable for a full end-to-end tuning.
- Compile the model.
- Train it with a very low learning rate. It's crucial to set a low learing rate as we only want to readapt pretrained features to work with our dataset and therefore large weight updates are not desirable at this stage.

The code is showed below:
```python
model.load_weights(best_weights_file) # load the best model saved by ModelCheckpoint
model.trainable = True
best_weights_file = "weights_fine_tuned.h5"
mc = ModelCheckpoint(best_weights_file, monitor='val_loss', mode='min', verbose=2,
                     save_best_only=True)
model.compile(loss='categorical_crossentropy', optimizer=Adam(1e-5), metrics=['accuracy'])
history = model.fit(datagenTrain.flow(xTrain, y_train_cat, batch_size=32), validation_data=(xTest, y_test_cat),
                    batch_size=32, callbacks= [es, mc], epochs=50, verbose=2)
```

## Results

In order to analyze the benefits introduced by the use of Transfer Learning and fine tuning, I compared the model described above with a simple CNN, trained from scratch with data augmentation, whose structure is showed below:
```python
def build_simple_CNN():
    model = Sequential()
    model.add(Conv2D(filters=32, kernel_size=(3,3),strides=(2,2), padding="valid",
                     activation="relu", input_shape=(IMG_SIZE,IMG_SIZE,CHANNELS)))
    model.add(MaxPooling2D(pool_size=(3,3),strides=(2,2)))
    model.add(BatchNormalization())
    model.add(Conv2D(filters=64,kernel_size=(3,3),strides=(2,2), padding="valid",
                     activation="relu"))
    model.add(Flatten())
    model.add(Dense(512, activation="relu"))
    model.add(Dropout(0.3))
    model.add(Dense(2, activation="softmax"))
    model.summary()
    return model
```
The following table shows a comparison between the performances achieved by the simple CNN and the proposed model:

|  | Accuracy | Precision | Recall | F1-Score |
|-|-|-|-|-|
| Simple CNN | 0.68 | 0.70 | 0.68 | 0.64 |
| Transfer Learning | 0.87 | 0.88 | 0.87 | 0.87 |
| Transfer Learning + Fine Tuning | 0.93 | 0.93 | 0.93 | 0.93 |

As we can easily see, the use of Tranfer Learning has led to much higher performances than a simple Convolutional Neural Network trained from scratch (*0.68 vs. 0.87 accuracy*). In addition, the fine tuning step has further improved performance significantly, reaching a *0.93 accuracy* on the test set.

Now let's take a closer look at the output of the model given some test images.
<p style="text-align: center"><b>Chihuahua</b></p>
<img src="cs.png" style="display: block; margin-left: auto; margin-right: auto; width: 100%; height: 100%"/>
<p style="text-align: center"><b>Pug</b></p>
<img src="ps.png" style="display: block; margin-left: auto; margin-right: auto; width: 100%; height: 100%"/>
Good job! The model is able to correctly classify dog images according to the breed with a high confidence level.

## Special guest

Lastly, we can test our breed classifier with external images (this is the funniest part). To do this I took some photos of my girlfriend's Chihuahua, **Emy**.
Let's see what our model says about this beautiful puppy:
<img src="emy.png" style="display: block; margin-left: auto; margin-right: auto; width: 100%; height: 100%"/>
Great! The model correctly classifies our cute Emy as a Chihuahua :clap::clap:
<hr>
You can find the full code on GitHub at this <a href="https://github.com/rcantini/Dog-breed-classification" target="_blank">link</a>.