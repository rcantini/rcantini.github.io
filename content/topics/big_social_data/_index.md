+++
title = "Big Social Data Analysis"

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
Riccardo Cantini’s research in big social data analysis explores how detailed user information from social media can be leveraged to uncover users’ perceptions of real-world events, offering data-driven insights into socio-political phenomena. His work addresses critical issues including reliability, language barriers, and dynamicity, while also tackling the challenges related to resource-intensive computation.

<h3>Political Polarization in Big Social Data</h3>
Cantini’s research in this field is primarily centered on politically polarized big social data, mainly those generated during election campaigns and referenda. A primary focus is determining the political leanings of social media users by analyzing the intricate dynamics of the multifaceted online political discourse. Key contributions include <i><a href="/publication/iom-2020/">IOM-NN (Iterative Opinion Mining using Neural Networks)</a></i>, a semi-supervised methodology that employs feed-forward neural networks to estimate the political polarization of social users during political events. This tool offers an accurate, fast, and cost-effective alternative to traditional opinion polls, also capturing sentiments on sensitive topics that users might avoid addressing openly. This methodology was further developed to examine the relationship between user polarization and sentiment toward political candidates, modeling political support across a broad spectrum of emotions. Topic modeling enhances this process, providing a richer representation of online conversations and enabling a comprehensive <i><a href="/publication/snam-usa_2022/">analysis workflow</a></i> for polarized social data. Cantini’s research also addressed challenges related to the influence of social bots on legitimate users and temporal dynamics in voting predictions. Specifically a novel methodology was introduced, termed <i><a href="/publication/bdcc-2022/">TIMBRE (Time-aware Opinion Mining via Bot Removal)</a></i>, which estimates political polarization amidst temporal fluctuations and bot malicious activity, achieving a reliable estimate of user polarization. Furthermore, the integration of information diffusion and influence maximization with polarization analysis is explored through <i><a href="/publication/osnem-2021/">WABC (Weighted Artificial Bee Colony)</a></i>, a bio-inspired algorithm designed to identify the key influencers in a politically polarized social network and uncover the primary information diffusion strategies employed by each faction during the political campaign.

<h3>Big Data Frameworks and ML-based Optimizations</h3>
This research addresses the computational challenges posed by the high volume and velocity of big social data by focusing on the efficient execution of data-intensive applications in high-performance distributed environments. A primary contribution is a detailed <i><a href="/publication/journal-big-data-2022/">review</a></i> of scalable tools and paradigms, culminating in a published <i><a href="/publication/programming-big-data-book/">book</a></i> on big data programming. This book serves as a practical guide for developers, aiding in the selection of optimal solutions based on application requirements and available resources.

To optimize parallel and distributed applications, Cantini’s research introduces novel techniques for workflow task scheduling and data partitioning. For task scheduling, the <i><a href="/publication/future-internet-2021/">IIWM (Intelligent In-memory Workflow Manager)</a></i> was proposed, balancing task parallelism and memory usage to minimize data spilling and improve application throughput. By leveraging machine learning to predict task memory needs and execution times, IIWM applies a heuristic bin-packing solution to generate effective schedules. Experiments conducted with Apache Spark demonstrate significant improvements in workflow performance compared to traditional approaches. In the area of data partitioning, a novel machine learning-based methodology was developed, named <i><a href="/publication/journal-big-data-2024-blest-ml/">BLEST-ML (BLock size ESTimation through Machine Learning)</a></i>. This approach effectively estimates optimal data block sizes for hybrid partitioning, optimizing the execution of data-parallel applications on large-scale infrastructures with minimal resource and domain knowledge requirements. Evaluations using the dislib library of PyCOMPSs, conducted in diverse environments—including the MareNostrum 4 supercomputer at the Barcelona Supercomputing Center (BSC)—reveal substantial performance gains and reductions in execution time.
</div>
</div>