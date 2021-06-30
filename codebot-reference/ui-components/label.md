---
layout: page
title: Label
permalink: /codebot-reference/ui-components/label
parent: UI Component Reference
grand_parent: CodeBot Reference
nav_order: 1
---

# UI Component Reference: Label

The `label` component is quite versatile. It can be used as a simple text prompt ("Enter your name" etc), for multi-line paragraphs, and for headings. The text can be static or made dynamic by linking it to a domain class & attribute or some other UI component.

> To bind a label to a component or link it to a domain attribute, see [State-bound Components](../../codegen-process-guide/UX/state-bound-components) and [Data-linked Components](../../codegen-process-guide/UX/data-linked-components) in the tutorial.

## Creating a label

To add a label to the wireframe in EA, add a `Label` component to the wireframe. `Label` can be found in the Toolbox under `Controls`, in the `UX Design` > `Wireframes` perspective.

## Creating a heading or sub-heading

To create a heading or sub-heading:

1. Add a `Label` component to the wireframe
2. Add a `css class` tag, with the value `h1` or `h2` (and so on up to `h6`)
3. In the wireframe editor, also set the font size to 18 (for h1) or 14 (for h2)

The third step is optional, but it helps to keep the wireframe and generated page looking alike.


## Setting the static label text

The easiest way to set the label text is to use the `name` property. EA shows the name as the label text on the wireframe.

As with all components, CodeBot uses the name as the component name in the generated code. However if the label is quite long or contains many non-alphanumeric characters (or "worst case" if it's all non-alphanumeric, e.g. "---------------"), this may not be ideal. In this case, you can give the label a "normal" name e.g. "divider", and put the text in a tagged value called `text`. The label will be displayed as "divider" in the wireframe, but will be displayed correctly in the generated UI.



## Tagged values

The `Label` component is primarily configured through the following tagged values:

| Tag name      | Values            | Default value | Notes                          |
| ------------- | ----------------- | ------------- | ------------------------------ |
| `text` | string value | If absent, the component name is used | The label text. |
| `css class`   | Any CSS class name, without a preceding `.`  |  | See the notes above about creating a heading or sub-heading. |
| `variant`   | Any "standard" Bootstrap variant value - see Variant in the [Tagged Values reference](../tagged-values) |  | For React, this will turn the label into an "Alert" component, with a background and text colour matching the variant. Useful for callouts, notes and static warnings ("Clicking OK will delete all your data"). |


