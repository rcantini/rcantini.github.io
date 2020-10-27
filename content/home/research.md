+++
widget = "research"  # The name of the widget that you created.
headless = true  # This file represents a page section.
#active = true  # Activate this widget? true/false
weight = 25 # Order that this section will appear in.

title = "Research Topics"
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

My research mainly focuses on the development of innovative algorithms and methodologies for the analysis of Big Data, especially those coming from the main social media, which provide a massive amount of opinion-rich multi-modal data effectively exploitable for extracting valuable information in different application contexts.
Particular attention is paid to:
<ul>
  <li>The use of Deep Learning and Natural Language Processing models for developing Sentiment Analysis and Opinion Mining techniques aimed at analyzing the mood of social users and their opinion regarding a specific topic/event of interest.</li>
  <li>Hashtag Recommendation, for developing models capable of predicting hashtags for posts that do not have any, in order to enrich the information content of social data involved in different mining processes.</li>
  <li>Information spread models and Influence maximization techniques, aimed at understanding how information flows within a social network and finding a small set of users that maximize the spread of influence.</li>
  <li>Techniques for integrating the classical centralized Cloud Computing architectures with the most recent IoT and Edge/Fog Computing solutions, which focus on manage data close to their source, allowing context-awareness, latency reduction and bandwidth saving.</li>
  <li>Data management optimization in scientific workflows</li>
</ul>
