---
title: "XAI-driven Knowledge Distillation of Large Language Models for Efficient Deployment on Low-Resource Devices"
date: 2024-04-19
publishDate: 2024-04-16
authors: ["Riccardo Cantini", "Alessio Orsino", "Domenico Talia"]
publication_types: ["2"]
abstract: "Large Language Models (LLMs) are characterized by their inherent memory inefficiency and compute-intensive nature, making them impractical to run on low-resource devices and hindering their applicability in edge AI contexts. To address this issue, Knowledge Distillation approaches have been adopted to transfer knowledge from a complex model, referred to as the teacher, to a more compact, computationally efficient one, known as the student. The aim is to retain the performance of the original model while substantially reducing computational requirements. However, traditional knowledge distillation methods may struggle to effectively transfer crucial explainable knowledge from an LLM teacher to the student, potentially leading to explanation inconsistencies and decreased performance. This paper presents DiXtill, a method based on a novel approach to distilling knowledge from LLMs into lightweight neural architectures. The main idea is to leverage local explanations provided by an eXplainable Artificial Intelligence (XAI) method to guide the cross-architecture distillation of a teacher LLM into a self-explainable student, specifically a bi-directional LSTM network.
Experimental results show that our XAI-driven distillation method allows the teacher explanations to be effectively transferred to the student, resulting in better agreement compared to classical distillation methods, thus enhancing the student interpretability. Furthermore, it enables the student to achieve comparable performance to the teacher LLM while also delivering a significantly higher compression ratio and speedup compared to other techniques such as post-training quantization and pruning, which paves the way for more efficient and sustainable edge AI applications."
featured: true
publication: "*Journal of Big Data*, vol. 11, no.63, 2024"
# url_pdf: "..."
doi: "https://doi.org/10.1186/s40537-024-00928-3"
# Custom links:
# links:
# - name: Project
#   url: https://github.com/rcantini/BLEST-ML
#   icon_pack: fab
#   icon: github
# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: ""
  focal_point: ""
  preview_only: false

tags: ["Large Language Models", "Knowledge Distillation", "eXplainable Artificial Intelligence", "Machine learning", "Sustainable AI", "Low-resource devices"]
---
