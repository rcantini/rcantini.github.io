+++
widget = "research"  # The name of the widget that you created.
headless = true  # This file represents a page section.
#active = true  # Activate this widget? true/false
weight = 25 # Order that this section will appear in.

title = "Research"
subtitle = ""


[content]
  # Page type to display. E.g. post, talk, or publication.
  page_type = "research"
  
  
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
<h3><b>Main topics</b></h3>
The research activity of Riccardo Cantini focuses on Big Data analysis, with particular attention to data generated on major social media platforms. The main objective is to extract a wide range of information about users in order to shape their perception of real-world facts and events, thus providing a data-driven approach for a deeper understanding of socio-political phenomena.
In this context, cutting-edge machine learning and deep learning models and techniques are employed, with a specific emphasis on the use of Large Language Models, along with frameworks for parallel and distributed computing. Key applications include identifying discussion topics in online conversations, estimating the political polarization of social users, and exploring the connection between their polarization and the emotions expressed in their published content.
Another aspect addressed is the dynamism of social media conversations and the impact of misinformation on user discussions. To this end, topic-oriented techniques are developed for detecting misinformation in social media content, as well as time-adaptive models capable of effectively handling continuously evolving real-time scenarios.
Furthermore, the research activity focuses on how to effectively learn from limited amounts of data and with scarce computing resources. Several solutions are investigated, including techniques for efficient fine-tuning, models based on curriculum learning and meta-learning, edge AI techniques for energy-aware computing, and the utilization of machine learning to optimize the execution of data-intensive applications on parallel and distributed architectures.
<br>
<div style="text-align: justify">
<h3><b>Participation in research projects</b></h3>
<ul>
  <li>"<b>eFlows4HPC: enabling dynamic and Intelligent workflows in the future EuroHPC ecosystem</b>", funded by the European High-Performance Computing Joint Undertaking.</li>
  <li>"<b>ASPIDE: exAScale ProgramIng models for extreme Data procEssing</b>", funded by the European Union’s Horizon 2020 Research and Innovation Programme.</li>
  <li>"<b>Smart Macingo</b>", funded under the Calabria Regional Operational Program 2014-2020.</li>
</ul>
</div>
