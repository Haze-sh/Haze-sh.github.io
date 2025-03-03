---
# Leave the homepage title empty to use the site title
title: ""
date: 2022-10-24
type: landing

design:
  spacing: "3rem"

sections:
  - block: resume-biography-3
    content:
      username: admin
      text: ""
      button:
        text: السيرة الذاتيّة
        url: uploads/resume.pdf
    design:
      css_class: dark
      background:
        color: black
        image:
          filename: iced.jpg
          filters:
            brightness: 0.2
          size: cover
          position: center
          parallax: false
          text_color_light: true

  - block: markdown

  - block: collection
    id: news
    content:
      title: Recent News
      subtitle: ''
      text: ''
      # Page type to display. E.g. post, talk, publication...
      page_type: post
      # Choose how many pages you would like to display (0 = all pages)
      count: 5
      # Filter on criteria
      filters:
        author: ""
        category: ""
        tag: ""
        exclude_featured: false
        exclude_future: false
        exclude_past: false
        publication_type: ""
      # Choose how many pages you would like to offset by
      offset: 0
      # Page order: descending (desc) or ascending (asc) date.
      order: desc
    design:
      # Choose a layout view
      view: date-title-summary
      # Reduce spacing
      spacing:
        padding: [0, 0, 0, 0]
---
