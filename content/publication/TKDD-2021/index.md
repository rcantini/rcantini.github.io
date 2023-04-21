---
title: "Learning sentence-to-hashtags semantic mapping for hashtag recommendation on microblogs"
date: 2021-05-06
publishDate: 2021-05-06
authors: ["Riccardo Cantini", "Fabrizio Marozzo", "Giovanni Bruno", "Paolo Trunfio"]
publication_types: ["2"]
abstract: "The growing use of microblogging platforms is generating a huge amount of posts that need
effective methods to be classified and searched. In Twitter and other social media platforms, 
hashtags are exploited by users to facilitate the search, categorization and spread of posts. 
Choosing the appropriate hashtags for a post is not always easy for users, and therefore posts 
are often published without hashtags or with hashtags not well defined. To deal with this issue, 
we propose a new model, called HASHET (HAshtag recommendation
using Sentence-to-Hashtag Embedding Translation), aimed at suggesting a relevant set of hashtags
for a given post. HASHET is based on two independent latent spaces for embedding the text of a post and
the hashtags it contains. A mapping process based on a multilayer perceptron is then used for learning a
translation from the semantic features of the text to the latent representation of its hashtags. We evaluated
the effectiveness of two language representation models for sentence embedding and tested different search
strategies for semantic expansion, finding out that the combined use of BERT (Bidirectional Encoder Representation
from Transformer) and a global expansion strategy leads to the best recommendation results.
HASHET has been evaluated on two real-world case studies related to the 2016 United States presidential
election and COVID-19 pandemic. The results reveal the effectiveness of HASHET in predicting one or
more correct hashtags, with an average F-score up to 0.82 and a recommendation hit-rate up to 0.92. Our
approach has been compared to the most relevant techniques used in the literature (generative models, unsupervised
models and attention-based supervised models) by achieving up to 15% improvement in F-score
for the hashtag recommendation task and 9% for the topic discovery task."
featured: true
publication: "*ACM Transactions on Knowledge Discovery from Data*"
# url_pdf: "files/papers/journals/HASHET_TKDD_online.pdf"
doi: "10.1145/3466876"


# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: ""
  focal_point: ""
  preview_only: false


tags: ["Deep Neural Networks", "Hashtag Recommendation", "Sentence Embedding", "Word Embedding", "Social Media"]

---
