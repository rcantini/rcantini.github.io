---
title: 'An overview of current research on hashtag recommendation'
subtitle: 'How to suggest a consistent set of hashtags for a microblog post'
summary: With the fast growing of microblog services, several NLP techniques have been developed for learning the representation of microblog posts and recommending pertinent hashtags. In what follows I'll introduce some of the most effective state-of-art approaches in this field.
date: 2020-07-16T18:10:09+02:00
draft: false
math: true
disable_comments: true
markup: kramdown
lastmod: 2020-07-16T18:10:09+02:00
authors:
- admin
tags:
- Deep Neural Networks
- Hashtag Recommendation
- Sentence Embedding
- Word Embedding
- Social Media
---

## Introduction

Social media platforms have become part of everyday life, allowing the interconnection of a large number of users. Their intensive use leads to the generation of a huge amount of data, which hides a high exploitable intrinsic value.  One of the most widely used data sources comes from microblogging services such as Twitter, Facebook and Instagram. This type of publication generates a large amount of posts which leads to the need for effective data categorization and search. To address this problem, tweets often include one or more hashtags. However, finding out the correct hashtags is not very easy for users, and tweets are often published without hashtags. This issue, which hinders the quality of search results, led to the rise of different techniques for hashtag recommendation, aimed at suggesting a consistent set of keywords for a given microblog post. In the following sections, four of the most effective state-of-art techniques are described, which follows different approaches such as topic modeling, clustering, topical co-attention and latent factor model like BPR matrix factorization used for personalized hashtag recommendation.

## Generative models: Latent Dirichlet Allocation & Gibbs sampling

[Godin et al.](https://dl.acm.org/doi/abs/10.1145/2487788.2488002) proposed a method for suggesting the top-\\(k\\) hashtags for a given post. They exploited **Latent Dirichlet Allocation** for finding out the underlying topic distribution, used for recommending general hashtags. Latent Dirichlet Allocation is a generative model which assumes that there exists a topic model with \\(T\\) topics underlying the data collection. Each document \\(m\\) has an associated multinomial topic distribution \\( \eta_m \\) over these topics. From this distribution, a topic \\( z \\)  can be determined for each word of the document. Next, a word for a topic \\( z \\)  can be sampled from the topic word distribution \\( \phi_z \\). Both \\( \eta \\)  and \\( \phi \\) are Dirichlet distributions with hyperparameters \\( \alpha \\)  and \\( \beta \\), respectively. For determining the model parameters, the authors used the **Gibbs sampling**, a Monte Carlo Markov Chain (MCMC) algorithm used to rapidly explore the space around a target distribution using repeated sampling. A topic \\( z_i \\) of a word \\( w_i \\), conditioned on the used words \\( \vec{w} \\)  of the model and the topic-word distribution \\( \vec{z_{\neg{i}}} \\), can be predicted as: 

$$
p(z_i = k|\vec{z_{\neg{i}}}, \vec{w}) \propto{\frac{n^w_{t,\neg{i}} + \beta_w}{\sum_{w=1}^{V}n^w_{t,\neg{i}} + \beta_w} * \frac{n^t_{m,\neg{i}} + \alpha_k}{\sum_{t=1}^{T}n^t_{m,\neg{i}} + \alpha_k}}
$$

where \\( n^w_t \\) denotes the topic-word count of topic \\( t \\) and word \\( w \\), and \\( n^t_m \\) the tweet-topic distribution. Specifically, they followed four main steps:
1. They used the Gibbs sampling algorithm for determining the LDA model parameters.
2. Given a tweet  \\(m\\), they used the topic-word count distribution \\( n^w_t \\) learned during the training phase for determining the topic distribution of \\(m\\) using Gibbs sampling again.
3. Based on the number \\(k\\) of hashtags to be recommended, they sampled for \\(k\\) times the obtained multinomial topic distribution, getting the number of keywords for each topic \\(t\\), i.e. \\( k_t \\), with \\( \sum_{t=0}^{T}k_t = k \\), where \\( T \\) is the number of topics discovered by LDA. 
4. The suggested hashtags will be the set of top-\\( k_t\\) words extracted from each topic \\(t\\) in ranked order.

## Unsupervised models: density-based clustering of tweet embeddings
[Ben Lachemi et al.](https://www.sciencedirect.com/science/article/pii/S1877050918301030) proposed a hashtag recommendation methodology based on the density-based clustering of the embedded representation of Twitter microblog posts, obtained using a **Word2Vec** model pre-trained on the Google News dataset. The key idea of this kind of representation is to map each word of a corpus of documents into a vector lying in a multidimensional latent space, in order to obtain dense representations of the words, whose distribution reflects their semantic relationships. The used clustering algorithm is **DBSCAN**, which exploits  the concept  of density for extracting clustering structures: it groups together points that are close to each other in high-density regions, marking as outliers points that lie alone in low-density regions. The density is related to the concept of core point, i.e. a point which has at least \\( min_{pts} \\) points in its \\( \epsilon \\)-neighborhood. The authors performed the following steps:
1. A given tweet is represented as the weighted average of its word embeddings. Given a tweet \\( t \\) composed by \\( n\\) words \\( w_1, w_2, ..., w_{n} \\), for each word \\( w_i\\) the Smooth Inverse Frequency (SIF) is computed as:
$$
s_i=\frac{a}{a+p(w_i)}
$$
where \\( a \\) is a constant and \\( p(w_i) \\) is the frequency of \\( w_i \\). Then, the latent representation of \\( t \\) is obtained as:
$$
v(t) = \frac{1}{n}\sum_{i=1}^{n}s_i\cdot v(w_i)
$$
where \\( v(w_i) \\) is the Word2Vec encoded representation of \\( w_i \\).
2. Latent representations of tweets are clustered according to their semantic similarity using the DBSCAN algorithm and the Manhattan distance metric. The authors set \\( min_{pts} = 1 \\) and estimated \\( \epsilon \\) as the average distance between each point and its nearest neighbor.
3. For each cluster a point is choosen and elected as centroid. 
4. For a given tweet \\( t \\), the most similar centroid \\( \hat{c} \\) is found according to the cosine distance: the related cluster \\( \hat{C} \\) will contain tweet semantically related to \\( t \\). The set of the hashtags used in the tweets in \\( \hat{C} \\) is computed and ordered by frequency. Finally the top-\\( k \\) hashtags of this set are returned.
 
## Neural attention models: topical co-attention networks
[Li et al.](https://www.sciencedirect.com/science/article/abs/pii/S0925231218314012) used an **attention-based neural network** to learn the representation of a microblog post. The basic idea behind the attention mechanism is to allows the model to focus on the relevant parts of the input sequence as needed. This goal is accomplished by determining a weight for each position that indicates the amount of attention that should be payed to it. Specifically, the authors proposed a novel **Topical Co-Attention Network** (TCAN) that models content attention and topic attention simultaneously and simmetrically: the content representations are used to guide the topic attention and the topic representation is used to guide content attention. The model mainly consists of four parts:
1. *LSTM-based sequence encoder*: a bidirectional LSTM which sequentially processes the embedded representation of each word of a tweet, generating a condensed vector representation which summarizes the information of the whole sequence. Specifically the forward and backward hidden states of the bidirectional LSTM are concatenated, obtaining \\( h_t = [\overrightarrow{h_t} ;\overleftarrow{h_t}] \\).
2. *Topic modeling*: topic models are a powerful technique for finding useful structures in a collection of documents. The main assumption is that a document is generated by a mixture of topics, each of which is a distribution over words in the vocabulary. To model the topics of microblogs, the author used Twitter LDA, which is the state-of-the-art topic model for short texts, based on the main assumption that microblog posts are mono-topic. After topic modeling, the model assigns a topic \\( z \\) to each microblog post \\( s \\). Then the top-\\( m \\) most probable words are extracted and this topical information about \\( s \\) is represented by a sequence of embedding vectors of topical words \\( b_1, b_1,  ..., b_m \\).
3. *Topical co-attention*: given all the hidden states \\( h_1, h_1,  ..., h_n \\) and the topical word embedding vectors \\( b_1, b_1,  ..., b_m \\) learned from topic modeling, the topical co-attention layer outputs a continuous context vector \\( vec \\) for each microblog post \\( s \\). This vector is obtained as follows:
	- An affinity matrix \\( E \in \mathcal{R}^{NxM} \\) is computed, with each element is determined as:
	$$
	e_{tk}=h_T^TW^{hb}b_k
	$$
	where \\( W^{hb} \\) is a trainable weight matrix, and \\( e_{tk} \\) is the attention weight between the hidden state \\( h_t \\) and the topical word embedding \\( b_k \\).
	- For the hidden state of a word \\( h_t \\), the relevant semantics in the global topic information (content-guided topic attention) is given by:
	$$\tilde{h_t}=\sum_{k=1}^{M}a_k^bb_k$$
	where \\(a_k^b\\) is the attention weight of \\( b_k \\), given by the softmax:
	$$a_k^b=\frac{exp(e_{tk})}{\sum_{j=1}^{M}exp(e_{tj})}$$
	- Similarly, topic-guided content attention is computed as:
	$$\tilde{b_k}=\sum_{t=1}^{N}a_t^hh_t$$
	where \\(a_t^h\\) is the attention weight of \\( h_t \\), given by the softmax:
	$$a_t^h=\frac{exp(e_{tk})}{\sum_{i=1}^{N}exp(e_{ik})}$$
	- The obtained vectors are further processed using average and max pooling, and concatenated obtaining the final context vector:
	$$
	vec = [v_{avg}^{h}; v_{avg}^{b}; v_{max}^{h}; v_{max}^{b}]
	$$
 4. *Softmax classifier*: the context vector is feed to a linear layer and then to a softmax classifier which outputs the probability distribution of all candidate hashtags. The authors trained the model using backpropagation, the cross-entropy loss function and the Adaptive Moment Estimation algorithm (ADAM), an adaptive optimization algorithm which compute a different learning rate for each parameter of the network.

## Latent factor models: Bayesian Personalized Rankinkg matrix factorization for personalized hashtag recommendation
[Li et al.](https://dl.acm.org/doi/10.1145/2932192) proposed joint probabilistic latent factor model for effectively capturing user implicit feedbacks and exploiting the rich microblog information, which integrates user adoption behaviors, user *microtopic* (i.e. hashtags) content and contextual information. 
Their model, namely **Microtopic Recommendation Model** (MTRM), builds on top of collaborative filtering, content analysis and feature regression, and consists og three main step:
1. *Modeling user-microtopic adoptions*: given a user vector \\(v_u\\) and a microtopic vector \\(v_u\\), they computed an affinity score which models user \\(u\\)'s preference to adopt microtopic \\(i\\) as: $$r_{u,i}=v_u^Tv_i+b_u+b_i$$
where \\(b_u\\) and \\(b_i\\) are user and item's biases to be learned. Then, they adopted an optimization ranking criterion, specifically the <b>Bayesian Personalized Ranking</b> (BPR), whose goal is to rank items according to user adoption. Let \\(\mathcal{P}\\) denote a set of triplets \\(<u, i, j>\\) derived from the training data where user \\(u\\) adopted hashtag\\(i\\) but not \\(j\\). The BPR criterion minimizes the following function: $$ min_\Theta \sum_{\langle u,i,j \rangle in \mathcal{P}}\hspace{0.1cm}ln(1+\mathcal{e}^{-(r_{u,i} - r_{u,j})}) $$ where \\(\Theta \\)  denotes the set of model parameters. Therefore, the above function maximes the difference between adopted and avoided microtopics.
2. *Modeling user and microtopic content*: the authors incorporated the content into the model by combining user's an microtopic’s posts into a pseudo-document. Then they modeled the pseuso-documents generation through Latent Dirichlet Allocation, by assuming that each hidden factor of users and microtopics has a corresponding multinomial word distribution \\(\phi_k\\), and is therefore related to a hidden LDA topic.
Each user has a distribution \\(\theta_u\\) over the \\(K\\) topics, derived from its hidden factor vector, given by:
$$\theta_{u,k}=\frac{exp(\mathcal{k}v_{u,k})}{\sum_{k^\prime}exp(\mathcal{k}v_{u,k^\prime})}$$
where \\(\mathcal{k}\\) is a parameter which controls the transformaion. All the words \\(w_u\\) in the pseudo-document representing a user \\(u\\) can be generated as:
$$p(w_u | \theta_u, \phi)=\prod_{n}\sum_{k=1}^K\Theta_{u,k}\phi_{k,w_{u,n}}$$ Microtopic distribution \\(\Theta_i\\) and the generation related to microtopic \\(i\\) can be derived similarly.
So, the second term to be added to the BPR optimization criterion is:
$$-(\sum_uln\hspace{0.1cm}p(w_u|\Theta)+\sum_iln\hspace{0.1cm}p(w_i|\Theta))$$
3. *Modeling user and microtopic attributes*: the authors incorporated also additional attibutes (e.g. gender) by exploiting a regression-based latent factorization method, which generates a latent factor vector for each attribute value. The main idea behind this kind of approach is that users or microtopics sharing the same attribute are likely to have similar vector in the latent factor space. They modeled user latent factors \\(v_u\\) as:
$$v_u=G_U^Ta_u + \sigma_u$$
where \\(G_u\\) is a regression coefficient matrix, \\(a_u\\) is the attribute vector of the user \\(u\\), which specifies a binary values for each attribute, and \\(\sigma_u\\) is u's deviation from regression.


Therefore, the overall objective function, which combines the above mentioned terms, is defined as follows:

$$min_\Theta & \sum_{\langle u,i,j \rangle in \mathcal{P}}\hspace{0.1cm}ln(1+\mathcal{e}^{-(r_{u,i} - r_{u,j})})$$
$$-\mu(\sum_uln\hspace{0.1cm}p(w_u|\Theta)+\sum_iln\hspace{0.1cm}p(w_i|\Theta))$$
$$+\lambda R(\Theta)$$

where the first term is the ranking optimization, the second the log likelihood of generating the content and the third an L2-norm regularization on the model parameters, while \\(\mu\\) and \\(\lambda\\) controls the contribution of each term on the overall loss function.