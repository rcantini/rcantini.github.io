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

My research mainly focuses on the development of innovative algorithms and methodologies for the analysis of Big Data, especially those coming from the main social media, in order to extract useful knowledge in different application contexts. Particular attention is paid to:

<ul>
  <li>Trajectory Mining, aimed at analyzing user behavior and their movements from geo-annotated data.</li>
  <li>Deep Learning and Natural Language Processing, in order to develop Sentiment Analysis and Opinion Mining techniques aimed at analyzing the mood of social users and their opinion regarding a specific topic of interest.</li>
  <li>Hashtag Recommendation, in order to develop systems based on Natural Language Processing able to suggest hashtags that enrich the information content of a set of posts involved in different mining processes.</li>
   <li>Techniques for the integration between the classic centralized architectures relating to Cloud Computing and the innovative Edge / Fog Computing solutions, which allow to manage data close to the source that originates them allowing a low latency response.
</ul>
