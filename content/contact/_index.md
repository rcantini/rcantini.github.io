+++
title = "Contact"
subtitle = ""

# Automatically link email and phone?
autolink = true

############################
## Contact details
##
## These details power the Contact widget (if enabled).
## Additionally, for organizations, these details may be used to enrich search engine results.
############################

# Enter contact details (optional). To hide a field, clear it to "".
email = "riccardo.cantini@unical.it"
phone = ""

# Address
# For country_code, use the 2-letter ISO code (see https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2 )
address = {street = "Cubo 41C, 5<sup>th</sup> floor, via P. Bucci", city = "Rende (CS)", region = "Calabria", postcode = "87036", country = "Italy", country_code = "IT"}

# Geographic coordinates
# To get your coordinates, right-click on Google Maps and choose "What's here?". The coords will show up at the bottom.
coordinates = {latitude = "39.36560", longitude = "16.22539"}

# Directions for visitors to locate you.
directions = ""

# Office hours
# A list of your office hours. To remove, set to an empty list `[]`.
office_hours = ["Office hours: send an email for booking an online meeting on Microsoft Teams"]

############################
## Maps
############################
[map]
  # To show your address on a map in the Contact widget, enter your latitude and longitude (above)
  # and choose a map provider below.
  #
  # To use Google Maps, set `engine` to 1 and enter your API key that can be obtained here:
  #   https://developers.google.com/maps/documentation/javascript/get-api-key
  # To use OpenStreetMap tiles, set `engine` to 2.
  # To use OpenStreetMap on a high traffic site, set `engine` to 3 and enter your API key that can be obtained here:
  #   https://www.mapbox.com/studio/account/tokens
  #
  # Map provider:
  #   0: No map
  #   1: Google Maps
  #   2: OpenStreetMap (Mapnik)
  #   3: OpenStreetMap (Mapbox)
  engine = 2
  api_key = ""
  zoom = 15

# Email form provider
#   0: Disable email form
#   1: Netlify (requires that the site is hosted by Netlify)
#   2: formspree.io
email_form = 0
+++