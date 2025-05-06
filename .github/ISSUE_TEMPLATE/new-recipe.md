---
name: "New Recipe Submission"
description: "Submit a new recipe for the digital cookbook. Please fill out all fields using the provided format."
title: "[Recipe] <Recipe Name>"
labels: [recipe]
body:
  - type: markdown
    attributes:
      value: |
        ## Recipe Submission Template
        Please copy the following front matter and fill in all fields. Paste it at the top of your recipe post.

        ```yaml
        ---
        layout: post
        title: "<Recipe Name>"
        date: YYYY-MM-DD
        categories: [<category1>, <category2>]
        tags: [<tag1>, <tag2>, ...]
        ingredients: [<ingredient1>, <ingredient2>, ...]
        excerpt: "<Short description for card previews>"
        prep_time: "<e.g. 10 min>"
        cook_time: "<e.g. 30 min>"
        servings: <number>
        dietary_info: "<e.g. Vegetarian, Gluten-Free, Dairy-Free>"
        ---
        ```

  - type: textarea
    id: recipe-content
    attributes:
      label: Recipe Content
      description: |
        Paste the full recipe content here, including sections for Ingredients, Instructions, Notes, Variations, etc.
      placeholder: |
        ## Ingredients
        - ...
        ## Instructions
        1. ...
        ## Notes
        - ...
        ## Variations
        - ...
    validations:
      required: true

  - type: checkboxes
    id: checklist
    attributes:
      label: Submission Checklist
      options:
        - label: I have filled out all required front matter fields.
          required: true
        - label: I have included a short excerpt/description for previews.
          required: true
        - label: I have reviewed the formatting and structure for consistency.
          required: true
