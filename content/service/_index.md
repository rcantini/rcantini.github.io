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
My research mainly focuses on the analysis of Big Data, especially those coming from the main social
media platforms, which provide a massive amount of opinion-rich multi-modal data effectively exploitable for
extracting valuable information about users’ dynamics, behavior, and opinion. In particular, the scope of
my research is twofold: one the one hand to develop innovative methodologies and algorithms for the analysis of Big Social Data;
on the other hand to design and implement novel techniques to enable their efficient execution in high-performance distributed environments.
<br>
I produced several interesting results in both research directions mentioned above, in a wide range of
application domains, including: political event analysis, opinion mining, polarization and emotion analysis, topic
detection and tracking, and hashtag recommendation. I also investigated how polarization analysis techniques can be combined with information diffusion and influence maximization models, 
how to effectively learn from poorly supervised datasets, and how to use machine learning for optimizing the execution of data-intensive applications.
<br>
<div style="text-align: justify">
<h3><b>Participation in research projects</b></h3>
<ul>
  <li><b>"eFlows4HPC: enabling dynamic and Intelligent workflows in the future EuroHPC ecosystem"</b>, funded by the European High-Performance Computing Joint Undertaking. The aim of the research is the use of machine learning techniques for enabling the efficient execution of data-intensive workflows in HPC environments.</li>
  <li><b>"ASPIDE: exAScale ProgramIng models for extreme Data procEssing"</b>, funded by the European Union’s Horizon 2020 Research and Innovation Programme. The aim of the research is the development of in-memory techniques for the efficient execution of data-intensive applications on Exascale architectures.</li>
  <li><b>"Smart Macingo"</b>, funded under the Calabria Regional Operational Program 2014-2020. The aim of the research is the definition and implementation of data mining techniques for estimating the price of transport services.</li>
</ul>
</div>

