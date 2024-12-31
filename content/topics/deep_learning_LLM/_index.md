+++
title = "Deep Learning and Large Language Models"

[content]
  # Page type to display. E.g. post, talk, or publication.
  page_type = "post"
  
  # Choose how many pages you would like to offset by
  offset = 0

  # Page order. Descending (desc) or ascending (asc) date.
  order = "desc"

  # Filter posts by a taxonomy term.
  [content.filters]
    tag = ""
    category = ""
    publication_type = ""
    exclude_featured = false

[design]
  # Choose how many columns the section has. Valid values: 1 or 2.
  columns = "1"


[background]
  # Background color.
  color = "navy"
  
  # Background gradient.
  gradient_start = "#4bb4e3"
  gradient_end = "#2b94c3"
  
  # Background image.
  image = "background.jpg"  # Name of image in `static/img/`.
  image_darken = 0.6  # Darken the image? Range 0-1 where 0 is transparent and 1 is opaque.

  # Text color (true=light or false=dark).
  text_color_light = true

[image]
placement = 1.0
caption = "Photo by [Academic](https://sourcethemes.com/academic/)"
focal_point = "Center"
preview_only = false

+++
<div style="text-align: justify">
Riccardo Cantini’s research in deep learning explores the potential of Transformer-based large language models (LLMs), such as BERT and GPT, showcasing their versatility across diverse domains. Sustainability is a central theme in this research area, emphasizing green awareness and promoting the efficient, fair, and trustworthy use of LLMs.

<h3>LLM Applications</h3>
Riccardo Cantini’s research in this field introduces several contributions, with a particular emphasis on social media contexts and real-world use cases. In the hashtag recommendation field, a novel BERT based methodology was developed, namely <i><a href="/publication/tkdd-2021/">HASHET (HAshtag recommendation using Sentence-to-Hashtag Embedding Translation)</a></i>. It employs dual latent spaces to embed the textual content of posts and their corresponding hashtags, learning to map semantic features of text to latent hashtag representations for a more accurate and scalable recommendation process. LLMs were also employed to tackle the spread of false information in online social media discourse. Specifically, a novel methodology was designed, termed <i><a href="/publication/ml-journal-2024/">TM-FID (Topic-oriented Multimodal False Information Detection)</a></i>, which combines false information detection with neural topic modeling within a semi-supervised multimodal framework. By jointly leveraging textual and visual information in online news, TM-FID provides insights into how false information influences specific discussion topics, enabling a comprehensive and fine-grained understanding of its spread and impact on social media conversations. LLMs were also leveraged in <i><a href="/publication/aiai-2024/">automated reporting</a></i> from social posts, with applications ranging from analyzing COVID-related discussions to enhancing <i><a href="/publication/osnem_llm-disaster_2024/">emergency management</a></i> during natural disasters. To ensure high-quality outputs, LLMs are enhanced with information across dimensions such as sentiment, emotion, and topic, extracted from user-generated content through fine-tuning and in-context learning approaches.

The potential of LLMs has also been explored in the healthcare domain, investigating how explainable AI (XAI) models can present technical results in a human-readable format through seamless integration with generative AI, improving accessibility for healthcare professionals. This approach was applied in two key areas: interpretable breast cancer grade prediction using genomic data and explainable depression detection from social media posts. In the former, explanations are achieved using interpretable-by-design machine learning models based on randomized trees. For the latter, explanations are generated using <i><a href="/publication/bert-xdd-preprint/">BERT-XDD (BERT-based eXplainable Depression Detection)</a></i>, a novel self-explainable model that integrates BERTweet with a bi-directional Long Short-Term Memory (LSTM) network, producing classifications and explanations via masked attention.

<h3>Green-Aware and Sustainable AI</h3>
In this context, techniques for efficient fine-tuning are combined with curriculum learning, meta-learning, and knowledge distillation, enabling effective learning from limited data and scarce computing resources. Innovative methodologies have been proposed to enhance cross-architecture knowledge distillation from LLMs to more compute-efficient neural architectures. Notably, <i><a href="/publication/journal-big-data-2024-dixtill/">DiXtill (XAI-driven Knowledge Distillation)</a></i> introduces a novel approach to distilling explainable knowledge from a teacher LLM into a lightweight, self- explainable student model. DiXtill combines local explanations with traditional prediction-based supervision, yielding higher accuracy and interpretability compared to standard distillation techniques. Furthermore, it achieves superior compression ratios and speedups compared to approaches like post-training quantization and attention head pruning, enabling efficient deployment on resource-constrained devices and advancing sustainable edge AI applications. Expanding upon online knowledge distillation, a parameter-efficient meta-distillation approach was designed, combining the effectiveness of the learning-to-teach paradigm with the efficiency of Low-Rank Adaptation (LoRA) within a second-order learning framework.

Beyond computational efficiency, Cantini’s research also addresses social sustainability by examining biases and stereotypes in responses generated by LLMs across various scales. Through <i><a href="/publication/ds2024-llm-bias/">adversarial analysis</a></i>, hidden vulnerabilities in LLMs are probed, quantifying the effectiveness of different jailbreak attacks and exploring how model size influences filtering mechanisms and overall safety. By thoroughly characterizing LLM behavior under bias elicitation in terms of fairness and robustness, this analysis provides critical insights to promote the ethical design of AI systems. Similarly aimed at ensuring fairness in LLM output, retrieval-augmented generation (RAG) systems are explored, combining agentic designs with real-time retrieval and textual entailment to enhance the accuracy, fairness, and reliability of LLM responses. Finally, sustainability-related research encompasses the integration of green awareness into neural architecture search techniques and the development of interpretable energy estimation models for edge AI applications.
</div>
