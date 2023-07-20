+++
widget = "research"  # The name of the widget that you created.
headless = true  # This file represents a page section.
#active = true  # Activate this widget? true/false
weight = 25 # Order that this section will appear in.

title = ""
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
<h3><b>Research topics</b></h3>
My research focuses on analyzing big data from major social platforms to extract diverse information about users and shape their perceptions of facts and events, thus providing a data-driven approach for a deeper understanding of real-world phenomena. Key applications include identifying discussion topics in online conversations, estimating the political polarization of social users, and exploring the connection between polarization and emotions expressed in social posts.
To this aim, advanced machine and deep learning techniques are utilized, with a focus on Large Language Models.
Moreover, my research explores how to efficiently learn from scarce data and limited computational resources. Several solutions are currently investigated, including the use of meta-learning techniques, semi-supervised models based on curriculum learning, edge AI techniques for energy-aware computing, and the use of machine learning to optimize the execution of data-intensive applications on parallel and distributed architectures.
Additionally, my research deals with aspects like the dynamicity of online conversation and the impact of misinformation in user discussions, through the design of topic-oriented misinformation detection techniques and time-adaptive models that can effectively adapt to rapidly changing real-time environments.
<br>
<div style="text-align: justify">
<h3><b>Participation in research projects</b></h3>
<ul>
  <li><b>"eFlows4HPC: enabling dynamic and Intelligent workflows in the future EuroHPC ecosystem"</b>, funded by the European High-Performance Computing Joint Undertaking. The aim of the research is the use of machine learning techniques for enabling the efficient execution of data-intensive workflows in HPC environments.</li>
  <li><b>"ASPIDE: exAScale ProgramIng models for extreme Data procEssing"</b>, funded by the European Union’s Horizon 2020 Research and Innovation Programme. The aim of the research is the development of in-memory techniques for the efficient execution of data-intensive applications on Exascale architectures.</li>
  <li><b>"Smart Macingo"</b>, funded under the Calabria Regional Operational Program 2014-2020. The aim of the research is the definition and implementation of data mining techniques for estimating the price of transport services.</li>
</ul>
</div>
