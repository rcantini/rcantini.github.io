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
<h2><b>Research topics</b></h2>
My research mainly focuses on the development of innovative algorithms and methodologies for the analysis of Big Data, especially those coming from the main social media, which provide a massive amount of opinion-rich multi-modal data effectively exploitable for extracting valuable information in different application contexts.
Particular attention is paid to:
<ul>
  <li>Advanced machine and deep learning models and architectures, especially in the field of natural language processing.</li>
  <li>Sentiment analysis and opinion mining techniques, aimed at detecting the emotional state and opinion of social users regarding a specific topic/event of interest.</li>
  <li>Hashtag recommendation and topic modeling.</li>
  <li>Techniques for integrating the classical centralized cloud computing architectures with the most recent IoT and edge/fog computing solutions.</li>
  <li>The use of machine learning models for the optimization of large-scale scientific workflows.</li>
</ul>
</div>
<br>
<div style="text-align: justify">
<h2><b>Participation in research projects</b></h2>
<ul>
  <li><b>"eFlows4HPC: enabling dynamic and Intelligent workflows in the future EuroHPC ecosystem"</b>, funded by the European High-Performance Computing Joint Undertaking.<br><mark>Research activity</mark>: use of machine learning techniques for the optimization of data intensive scientific workflows. Particular attention is paid to the study and the implementation of hyperparameter optimization models, aimed at enabling the efficient execution of distributed and scalable algorithms in HPC environments.</li>
  <li><b>"ASPIDE: exAScale ProgramIng models for extreme Data procEssing"</b>, funded by the European Union’s Horizon 2020 Research and Innovation Programme.<br><mark>Research activity</mark>: development of in-memory techniques for the efficient execution of data intensive applications on Exascale architectures. The research is aimed in particular at defining and implementing a scheduling strategy for assigning application tasks to computing nodes, taking into account availability of data and resources.</li>
  <li><b>"Smart Macingo"</b>, funded under the Calabria Regional Operational Program 2014-2020.<br><mark>Research activity</mark>: definition and implementation of data mining techniques aimed at estimating the price of transport services.</li>
</ul>
</div>