---
layout: page
title: Label
permalink: /codebot-reference/ui-components/label
parent: UI Component Reference
grand_parent: CodeBot Reference
nav_order: 6
---

# UI Component Reference: Label

Display text, which can either be simple/static, or bound to a component such as a table's selected row. Turn a label into a heading by adding a `css class` tagged value with `h1`, `h2` etc (named after Bootstrap classes).

## Which wireframe component?

Depending which modeling tool you're using, add the following component from the palette into the wireframe:

| Tool    |  Wireframe component(s) |
| ------- |  ---------------------- |
| Enterprise Architect | Label |
| Magic Draw | Label |


## Capabilities

|        |  Notes               |
| ------ |  ------------------- |
| Displays a single text value | The component can display an individual text value, which can be derived from a bound UI event (e.g. table row selection). |
| Reactive | The component can listen to UI events triggered by another component, via the `bind` tag or a dependency arrow. |

The `label` component is quite versatile. It can be used as a simple text prompt ("Enter your name" etc), for multi-line paragraphs, and for headings. The text can be static or made dynamic by linking it to a domain class & attribute or some other UI component.

## Creating a label

To add a label to the wireframe in EA, add a `Label` component to the wireframe. `Label` can be found in the Toolbox under `Controls`, in the `UX Design` > `Wireframes` perspective.

## Creating a heading or sub-heading

To create a heading or sub-heading:

1. Add a `Label` component to the wireframe
2. Add a `css class` tag, with the value `h1` or `h2` (and so on up to `h6`)
3. In the wireframe editor, also set the font size to 18 (for h1) or 14 (for h2)

The third step is optional, but it helps to keep the wireframe and generated page looking alike.


## Setting the static label text

Using EA, the easiest way to set the label text is to use the `name` property. EA shows the name as the label text on the wireframe. If you want the label to contain a whole paragraph, in EA set the `multiline` property to true.
(This doesn't affect how the UI element is generated, as it'll naturally word-wrap depending on the CSS styling).

Using MagicDraw, either use `name` as with EA, or use the `text` property. If `text` is non-empty, it'll be used instead of `name'.

As with all components, CodeBot uses the name as the component name in the generated code. However if the label is quite long or contains many non-alphanumeric characters (or "worst case" if it's all non-alphanumeric, e.g. "---------------"), this may not be ideal. In this case, you can give the label a "normal" name e.g. "divider", and put the text in a tagged value called `text`. The label will be displayed as "divider" in the wireframe, but will be displayed correctly in the generated UI.


## Tagged values

| Tag      | Allowed values | Notes               |
| -------- | -------------- | ------------------- |
| `bind`  |  | Makes this UI Element listen to another UI element for events (e.g. row item selected), via a Redux UI global state selector.<br><br>This tag is the same as connecting the elements with a Dependency arrow. However, you can use this tag, for example, if the other UI element is on a different wireframe.<br><br>The following component types can be 'state-bound' (i.e. listen to another UI Element via the bind tag or dependency arrow): <br><br>Button, Checkbox, ComboBox, Link, ListBox, MapPicker, MediaPlayer, PasswordField, RangeInput, Table, TextArea, TextField |
| `display text`<br>&nbsp;or:<br>&nbsp;`text`  |  DEFAULT: the UI element name | Text to display, if not using the component name.<br><br>For EA wireframes the element name is normally used; however this tag will override that if the name needs to be different, e.g. to avoid duplicate element names, or if the text won't map well to variable names etc. |
| `read only`  |  DEFAULT: no | If true (or yes), the input element can't be edited; updates are only via a bound element such as a ComboBox. |
| `css class`  | Any CSS class name, without a preceding `.` | Adds the specified CSS class (or classes) to the UI element. If you define a class in a custom CSS file, you can apply it to a component using this tag. CodeBot will also recognise any 'standard' Bootstrap CSS classes such as `h1`, `h2` etc; their defined behaviour will be carried over to any future UI platforms that CodeBot generates. |
| `variant css class`  |  |  |
| `cell css class`  |  |  |
| `variant`<br>&nbsp;or:<br>&nbsp;`appearance`  | Must be one of: primary, secondary, success, danger, warning, info, light, dark, link | Changes a UI Element's appearance. The allowed values are based on Bootstrap's variant CSS classes.<br><br>For React Labels, this will turn the label into an "Alert" component, with a background and text colour matching the variant. Useful for callouts, notes and static warnings ("Clicking OK will delete all your data"). |

[Tagged values for all model elements including UI component types](../tagged-values)

## Also see

* [Binding a label to a component](../../codegen-process-guide/ux/state-bound-components)
* [Linking a label to a domain attribute](../../codegen-process-guide/ux/data-linked-components)

