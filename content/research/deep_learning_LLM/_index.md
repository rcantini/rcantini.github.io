+++
title = "Research"
subtitle = ""


[content]
  # Page type to display. E.g. post, talk, or publication.
  page_type = "publication"
  
  
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
lll
Riccardo Cantini’s research spans two distinct areas: deep learning, focusing on large language models (LLMs) and sustainable artificial intelligence, and distributed big social data analysis, targeting politically polarized data and the efficient execution of data-intensive applications in high-performance distributed environments.

<h3><b>Deep Learning and Large Language Models</b></h3>
Riccardo Cantini’s research in deep learning explores the potential of Transformer-based large language models (LLMs), such as BERT and GPT, showcasing their versatility across diverse domains. Sustainability is a central theme in this research area, emphasizing green awareness and promoting the efficient, fair, and trustworthy use of LLMs.

<h3>LLM Applications</h3>
Riccardo Cantini’s research in this field introduces several contributions, with a particular emphasis on social media contexts and real-world use cases. In the hashtag recommendation field, a novel BERT based methodology was developed, namely HASHET (HAshtag recommendation using Sentence-to-Hashtag Embedding Translation) [9]. It employs dual latent spaces to embed the textual content of posts and their corresponding hashtags, learning to map semantic features of text to latent hashtag representations for a more accurate and scalable recommendation process. LLMs were also employed to tackle the spread of false information in online social media discourse[2], [16]. Specifically, a novel methodology was designed, termed TM-FID (Topic-oriented Multimodal False Information Detection), which combines false information detection with neural topic modeling within a semi-supervised multimodal framework. By jointly leveraging textual and visual information in online news, TM-FID provides insights into how false information influences specific discussion topics, enabling a comprehensive and fine-grained understanding of its spread and impact on social media conversations. LLMs were also leveraged in automated reporting from social posts, with applications ranging from analyzing COVID-related discussions to enhancing emergency management during natural disasters[1], [15]. To ensure high-quality outputs, LLMs are enhanced with information across dimensions such as sentiment, emotion, and topic, extracted from user-generated content through fine-tuning and in-context learning approaches. The potential of LLMs has also been explored in the healthcare domain, investigating how explainable AI (XAI) models can present technical results in a human-readable format through seamless integration with generative AI, improving accessibility for healthcare professionals. This approach was applied in two key areas: interpretable breast cancer grade prediction using genomic data and explainable depression detection from social media posts. In the former, explanations are achieved using interpretable-by-design machine learning models based on randomized trees. For the latter, explanations are generated using BERT-XDD (BERT-based eXplainable Depression Detection), a novel self-explainable model that integrates BERTweet with a bi-directional Long Short-Term Memory (LSTM) network, producing classifications and explanations via masked attention.

<h3>Green-Aware and Sustainable AI</h3>
In this context, techniques for efficient fine-tuning are combined with curriculum learning, meta-learning, and knowledge distillation, enabling effective learning from limited data and scarce computing resources. Innovative methodologies have been proposed to enhance cross-architecture knowledge distillation from LLMs to more compute-efficient neural architectures. Notably, DiXtill (XAI-driven Knowledge Distillation) [3] introduces a novel approach to distilling explainable knowledge from a teacher LLM into a lightweight, self-explainable student model. This method combines local explanations with traditional prediction-based supervision, yielding higher accuracy and greater interpretability compared to standard distillation techniques. Furthermore, DiXtill achieves superior compression ratios and speedups compared to approaches like post training quantization and attention head pruning, enabling efficient deployment on resource-constrained devices and advancing sustainable edge AI applications. Expanding upon online knowledge distillation, a parameter-efficient meta-distillation was also designed, combining the learning-to-teach paradigm with the efficiency of Low-Rank Adaptation (LoRA) within a second-order parameter-efficient learning framework. Beyond computational efficiency, Cantini’s research also addresses social sustainability by examining biases and stereotypes in responses generated by LLMs across various scales[13]. Through adversarial analysis, hidden vulnerabilities in LLMs are probed, quantifying the effectiveness of different jailbreak attacks and exploring how model size influences filtering mechanisms and overall safety. By thoroughly characterizing LLM behavior under bias elicitation in terms of fairness and robustness, this analysis provides critical insights to promote the ethical design of AI systems. Similarly aimed at ensuring fairness in LLM output, retrieval-augmented generation (RAG) systems are explored, combining agentic designs with real-time retrieval and textual entailment to enhance the accuracy, fairness, and reliability of LLM responses. Finally, sustainability-related research encompasses the integration of green awareness into neural architecture search techniques and the development of interpretable energy estimation models for edge AI applications.

<h3><b>Distributed Big Social Data Analysis</b></h3>
Riccardo Cantini’s research in big social data analysis explores how detailed user information from social media can be leveraged to uncover users’ perceptions of real-world events, offering data-driven insights into socio-political phenomena. His work addresses critical issues including reliability, language barriers, and dynamicity, while also tackling the challenges related to resource-intensive computation.

<h3>Political Polarization in Big Social Data</h3>
Cantini’s research in this field is primarily centered on politically polarized big social data, mainly those generated during election campaigns and referenda. A primary focus is determining the political leanings of social media users by analyzing the intricate dynamics of the multifaceted online political discourse. Key contributions include IOM-NN (Iterative Opinion Mining using Neural Networks) [12], a semi-supervised methodology that employs feed-forward neural networks to estimate the political polarization of social users during political events. This tool offers an accurate, fast, and cost-effective alternative to traditional opinion polls, also capturing sentiments on sensitive topics that users might avoid addressing openly. This methodology was further developed to analyze the relationship between user polarization and sentiment toward political candidates, modeling political support across a broad spectrum of emotions. Topic modeling enhances this process, providing a richer representation of online conversations and enabling a comprehensive workflow for analyzing polarized data[7]. Cantini’s research also addressed challenges related to the influence of social bots on legitimate users and temporal dynamics in voting predictions. Specifically a novel methodology was introduced, termed TIMBRE (Time-aware Opinion Mining via Bot Removal)[6], which estimates political polarization amidst temporal fluctuations and bot malicious activity, achieving a reliable estimate of user polarization. Furthermore, the integration of information diffusion and influence maximization with polarization analysis is explored through WABC (Weighted Artificial Bee Colony) [10], a bio-inspired algorithm designed to identify the key influencers in a politically polarized social network and uncover the primary information diffusion strategies employed by each faction during the political campaign.

<h3>Big Data Frameworks and ML-based Optimizations</h3>
This research addresses the computational challenges posed by the high volume and velocity of big social data by focusing on the efficient execution of data-intensive applications in high-performance distributed environments. A primary contribution is a detailed evaluation of scalable tools and paradigms[5], culminating in a published book on big data programming[20]. This book serves as a practical guide for developers, aiding in the selection of optimal solutions based on application requirements and available resources. To optimize parallel and distributed applications, Cantini’s research introduces novel techniques for workflow task scheduling and data partitioning. For task scheduling, the IIWM (Intelligent In-memory Workflow Manager)[11] was proposed, balancing task parallelism and memory usage to minimize data spilling and improve application throughput. By leveraging machine learning to predict task memory needs and execution times, IIWM applies a heuristic bin-packing solution to generate effective schedules. Experiments conducted with Apache Spark demonstrate significant improvements in workflow performance compared to traditional approaches. In the area of data partitioning, a novel machine learning-based methodology was developed, named BLEST-ML (BLock size ESTimation through Machine Learning)[4]. This approach effectively estimates optimal data block sizes for hybrid partitioning, optimizing the execution of data-parallel applications on large-scale infrastructures with minimal resource and domain knowledge requirements. Evaluations using the dislib library of PyCOMPSs, conducted in diverse environments—including the MareNostrum 4 supercomputer at the Barcelona Supercomputing Center (BSC)—reveal substantial performance gains and reductions in execution time.

<br><br>
<div style="text-align: left">
<h3><b>Participation in Research Projects</b></h3>
<div class="media stream-item" style="margin-top: 40px;">
	<div class="mr-3">
		<a href="https://doi.org/10.1142/q0444" target="_blank">
			<img src="logos/FAIR_logo.png" alt="FAIR_LOGO" style="margin-top: 0px;"></a>
	</div>
	<div class="media-body">
		<h5 class="mb-0 mt-0"><a href="https://fondazione-fair.it/" target="_blank">
FAIR: Future Artificial Intelligence Research</a></h5>
		<div class="stream-meta article-metadata">
			<div>
				<span>Funded by the European Union's NextGenerationEU program</span>
			</div>
		</div>
	</div>
</div>
<div class="media stream-item">
	<div class="mr-3" style="margin-top:5px;">
		<a href="https://doi.org/10.1142/q0444" target="_blank">
			<img src="logos/eFlows4HPC_logo.png" alt="eFlows4HPC_logo" style="margin-top: 0px;"></a>
	</div>
	<div class="media-body">
		<h5 class="mb-0 mt-0"><a href="https://eflows4hpc.eu/" target="_blank">
eFlows4HPC: enabling dynamic and Intelligent workflows in the future EuroHPC ecosystem</a></h5>
		<div class="stream-meta article-metadata">
			<div>
				<span>Funded by the European High-Performance Computing Joint Undertaking</span>
			</div>
		</div>
	</div>
</div>
<div class="media stream-item">
	<div class="mr-3" style="margin-top:5px;">
		<a href="https://doi.org/10.1142/q0444" target="_blank">
			<img src="logos/ASPIDE_logo.png" alt="ASPIDE_logo" style="margin-top: 0px; margin-bottom:0px;"></a>
	</div>
	<div class="media-body">
		<h5 class="mb-0 mt-0"><a href="https://cordis.europa.eu/project/id/801091" target="_blank">
ASPIDE: exAScale ProgramIng models for extreme Data procEssing</a></h5>
		<div class="stream-meta article-metadata">
			<div>
				<span>Funded by the European Union’s Horizon 2020 Research and Innovation Program</span>
			</div>
		</div>
	</div>
</div>
