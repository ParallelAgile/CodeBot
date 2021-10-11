---
layout: page
title: Container
permalink: /codebot-reference/ui-components/container
parent: UI Component Reference
grand_parent: CodeBot Reference
nav_order: 4
---

# UI Component Reference: Container

Contains other UI elements, including other containers.<br><br>Use containers to manage your page layout; e.g. create a sidebar, page header/footer, or adjacent panels.<br><br>To turn a container into an input form, add a Button with an `action` tag, e.g. with the value `create`. The container should also be linked to a domain class.

## Which wireframe component?

Depending which modeling tool you're using, add the following component from the palette into the wireframe:

| Tool    |  Wireframe component(s) |
| ------- |  ---------------------- |
| Enterprise Architect | ClientArea |
| Magic Draw | Panel |


## Capabilities

|        |  Notes               |
| ------ |  ------------------- |
| Container | Can contain 'child' UI elements. |


## Tagged values

| Tag      | Allowed values | Notes               |
| -------- | -------------- | ------------------- |
| `justify`  | Must be one of: left, right, center | Text justification for the UI element container. |
| `css class`  | Any CSS class name, without a preceding `.` | Adds the specified CSS class (or classes) to the UI element. If you define a class in a custom CSS file, you can apply it to a component using this tag. CodeBot will also recognise any 'standard' Bootstrap CSS classes such as `h1`, `h2` etc; their defined behaviour will be carried over to any future UI platforms that CodeBot generates. |
| `variant css class`  |  |  |
| `cell css class`  |  |  |
| `variant`<br>&nbsp;or:<br>&nbsp;`appearance`  | Must be one of: primary, secondary, success, danger, warning, info, light, dark, link | Changes a UI Element's appearance. The allowed values are based on Bootstrap's variant CSS classes.<br><br>For React Labels, this will turn the label into an "Alert" component, with a background and text colour matching the variant. Useful for callouts, notes and static warnings ("Clicking OK will delete all your data"). |

[Tagged values for all model elements including UI component types](../tagged-values)

## Also see

* [Button component](button)

