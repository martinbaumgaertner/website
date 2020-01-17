+++
# A Projects section created with the Portfolio widget.
widget = "portfolio"  # See https://sourcethemes.com/academic/docs/page-builder/
headless = true  # This file represents a page section.
active = true# Activate this widget? true/false
weight = 35# Order that this section will appear. 

title = "Code"
subtitle = ""

[content]

page_type = "project"

filter_default = 0

[[content.filter_button]]
    name = "All"
    tag = "*"

  [[content.filter_button]]
    name = "Deep Learning"
    tag = "Deep Learning"

  [[content.filter_button]]
    name = "Other"
    tag = "Demo"

[design]
  # Choose how many columns the section has. Valid values: 1 or 2.
  columns = "2"

  # Toggle between the various page layout types.
  #   1 = List
  #   2 = Compact  
  #   3 = Card
  #   5 = Showcase
  view = 3

  # For Showcase view, flip alternate rows?
  flip_alt_rows = false

