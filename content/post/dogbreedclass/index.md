---
title: 'What breed is that puppy? Dog breed classification using Convolutional Neural Networks and Transfer Learning in Keras'
subtitle: 'How to exploit Convolutional Neural Networks and Transfer Learning for building a computer vision application that can distinguish a Chihuahua from a Pug'
summary: "In what follows, I'll show how to build a dog breed classifier based on Convolutional Neural Networks, which focuses on two particular breeds: Chihuahua and Pug. In order to cope with the small amount of traning data, the model exploits three main techniques: real time data augmentation, Transfer Learning and fine tuning."
date: 2020-11-28T00:00:00Z
draft: false
math: true
disable_comments: true
markup: kramdown
lastmod: 2020-11-28T00:00:00Z
authors:
- admin
tags:
- Convolutional Neural Networks
- Transfer Learning
- Dog Breed Classification
- Computer Vision
- Image Recognition
- Deep Learning
- Keras-Tensorflow
---

In what follows I'll show how to build a computer vision application with Keras and Tensorflow for classifying dog images according to their breed. The presented model focuses on two particular breeds, **Chihuahua** and **Pug**, and relies on Convolutional Neural Networks, a state-of-art deep learning model for the image classification task.

## Convolutional Neural Networks
**Convolutional neural networks** (*CNNs*) are a deep learning model inspired by the organization and functioning of the animal visual cortex.
Individual neurons are arranged so as to respond to partially overlapping regions that make up the visual field, called *receptive fields*.
These networks can learn a meaningful representation of a given image by automating the feature extraction process.
The classical architecture of a CNN consists of a series of particular layers:
- *Convolutional layer*: given an input image the convolution is carried out using a set of filters, called kernels, which are matrices of learnable weights. Convolution is performed using dot product between the filter and the portion of the image over which it is hovering; the filter is shifted according to a stride parameter and this process is repeated until the the entire image has been covered, generating an output volume composed by a set of convolved feature maps.
The convolution of a \\(3\times 3\\) kernel, with \\(stride=1\\) (one pixel at a time) applied to a single-channel \\(5\times 5\\) image is showed below:
<img src="conv.gif" style="display: block; margin-left: auto; margin-right: auto; width: 60%; height: 60%"/>
- *Relu layer*: Rectified Linear Unit is the typical activation function of convolutional levels, defined as \\(f(x) = max(0, x)\\).
This function has many interesting properties, including efficiency, robustness against weight saturation or vanishing gradient, as well as the sparse activation of artificial neurons, which mimics what happens in biological systems, where only few neurons activate simultaneously.
- *Pooling layer*: the role of this layer is to reduce the spatial size of the output volume from the convolutional layer, extracting rotational and positional invariant features. Dimensionality reduction is carried out using a kernel which moves upon the input matrices, taking the maximum (or the average) of the covered values.
- *Fully-connected layer*: the output of convolutional and pooling layers can be flattened and feed to a dense layer of fully connected neurons, in order to learn a non-linear combination of the learned features. Finally a softmax classifier can be used for determining a probability value for each class label.

## Chihuahua vs. Pug
Let's now move on how to use Convolutional Neural Networks in Keras in order to build our breed classifier, for distinguish a Chihuahua from a Pug. Our dataset is an extract from <a href="https://www.kaggle.com/c/dog-breed-identification">Dog Breed Identification</a>, and is composed by 152 Chihuahua and 200 Pug images.
Data are normalized and resized to a fixed shape of \\(350\times 350\\). Now let's look at some example images from our dataset:
<img src="dogs_example.png" style="display: block; margin-left: auto; margin-right: auto; width: 100%; height: 100%"/>
This is a really challenging classification task, as the pattern to be learned are quite complex and the training images are few compared to how many a CNN would need to learn meaningful features. In order to cope with the small amount of traning data, the model exploits three main techniques:
- Transfer Learning
- Real time data augmentation
- Fine tuning

## Transfer Learning
Transfer Learning technique consists of exploiting features learned on one problem, for dealing with a new similar problem: this way, the abilities of a pre-trained model can be transferred to one another. This technique is very usefull when data are not enough to build a full model from scratch, as in our case.
I exploited this strategy creating our dog breed classifier as follows:
- Load the pre-trained model: I used a VGG16 model which has been pre-trained on ImageNet, a +10 million image dataset from 1000 categories.
- Freeze VGG16 layers, so as to avoid destroying the information they contain during training.
- Add a multilayer perceptron on top of them, composed by two trainable fully connected layers, Dropout for preventing overfitting and a softmax classifier.
The Keras implementation of the model is showed below:
```python
def transfer_learning():
    vgg_conv = vgg16.VGG16(weights='imagenet', include_top=False, input_shape=(350, 350, 3))
    for layer in vgg_conv.layers[:]:
        layer.trainable = False
    model = Sequential()
    model.add(vgg_conv)
    model.add(Flatten())
    model.add(Dense(1024, activation='relu'))
    model.add(Dropout(0.5))
    model.add(Dense(512, activation='relu'))
    model.add(Dropout(0.5))
    model.add(Dense(2, activation='softmax'))
    model.summary()
    return model
```

## Training the model with real time data augmentation
Now our model is ready for the training step. As the amount of images available for training the model is small, we can use an ImageDataGenerator in order to obtain some additional training samples:
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
Now we can use our generator while training the model, obtaining data augmentation in real time:
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
The model has been trained using the *categorical_crossentropy* loss function and the *Adam* optimizer. Furthermore, in order to avoid overfitting, two callback functions are used for early stopping the learning process by monitoring the loss, storing the best model.

## Fine tuning

...
...
...

```python
model.load_weights(best_weights_file) # load the best saved model
model.trainable = True
best_weights_file = "weights_fine_tuned.h5"
mc = ModelCheckpoint(best_weights_file, monitor='val_loss', mode='min', verbose=2,
                     save_best_only=True)
model.compile(loss='categorical_crossentropy', optimizer=Adam(1e-5), metrics=['accuracy'])
history = model.fit(datagenTrain.flow(xTrain, y_train_cat, batch_size=32), validation_data=(xTest, y_test_cat),
                    batch_size=32, callbacks= [es, mc], epochs=50, verbose=2)
```

...
...
...


<p><span style="font-size:14.0pt;line-height:90%;font-family:
&quot;Open Sans&quot;,sans-serif">Link to the code on GitHub: <a href="https:https://github.com/rcantini/Dog-breed-classification" target="_blank">Dog-breed-classification</a></span></p>