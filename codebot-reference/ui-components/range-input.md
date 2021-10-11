---
layout: page
title: Range Input
permalink: /codebot-reference/ui-components/range-input
parent: UI Component Reference
grand_parent: CodeBot Reference
nav_order: 12
---

# UI Component Reference: Range Input

Numeric text input, with upper and lower bounds. To create, add a TextField (or Spinner if using MagicDraw), and then define the allowed range using a constraint, e.g. `0-9`.

## Which wireframe component?

Depending which modeling tool you're using, add the following component from the palette into the wireframe:

| Tool    |  Wireframe component(s) |
| ------- |  ---------------------- |
| Enterprise Architect | Text Field |
| Magic Draw | Spinner, Text Field |


## Capabilities

|        |  Notes               |
| ------ |  ------------------- |
| Single value input | The component allows a single value to be input. |
| Displays a single text value | The component can display an individual text value, which can be derived from a bound UI event (e.g. table row selection). |
| Domain data | The component can be linked to a domain class, via the `domain` tag or a dependency arrow. The component will show data loaded from the domain class' relevant API endpoint. |
| Reactive | The component can listen to UI events triggered by another component, via the `bind` tag or a dependency arrow. |
| Bind target | Other components can listen and react to this component's' UI events, via their `bind` tag or a dependency arrow pointing to this component. |


## Tagged values

| Tag      | Allowed values | Notes               |
| -------- | -------------- | ------------------- |
| `bind`  |  | Makes this UI Element listen to another UI element for events (e.g. row item selected), via a Redux UI global state selector.<br><br>This tag is the same as connecting the elements with a Dependency arrow. However, you can use this tag, for example, if the other UI element is on a different wireframe.<br><br>The following component types can be 'state-bound' (i.e. listen to another UI Element via the bind tag or dependency arrow): <br><br>Button, Checkbox, ComboBox, Link, ListBox, MapPicker, MediaPlayer, PasswordField, RangeInput, Table, TextArea, TextField |
| `domain`  |  | Links a component to a domain class, and optionally an attribute.<br><br>Depending on the component, it will then use the domain data in some way, e.g. to populate a table or listbox with domain data for selection.<br><br>The linked data will be loaded via the domain class' matching REST API endpoint, with loading state managed in the UI via a Redux domain selector.<br><br>Please note: This tag is the same as connecting the element to a domain class with a Dependency arrow. |
| `display domain`  |  | Specifies which domain class attribute to display.  For cases where the display attribute/relationship is different from the 'data' domain attribute/relationship. |
| `form domain`  |  | For Domain Chooser UI Elements (listbox, ComboBox), where the form attribute/relationship is different from the 'data' domain attribute/relationship, as two domain classes are involved. |
| `display text`<br>&nbsp;or:<br>&nbsp;`text`  |  DEFAULT: the UI element name | Text to display, if not using the component name.<br><br>For EA wireframes the element name is normally used; however this tag will override that if the name needs to be different, e.g. to avoid duplicate element names, or if the text won't map well to variable names etc. |
| `css class`  | Any CSS class name, without a preceding `.` | Adds the specified CSS class (or classes) to the UI element. If you define a class in a custom CSS file, you can apply it to a component using this tag. CodeBot will also recognise any 'standard' Bootstrap CSS classes such as `h1`, `h2` etc; their defined behaviour will be carried over to any future UI platforms that CodeBot generates. |
| `variant css class`  |  |  |
| `cell css class`  |  |  |
| `default value`<br>&nbsp;or:<br>&nbsp;`default`  |  |  |
| `variant`<br>&nbsp;or:<br>&nbsp;`appearance`  | Must be one of: primary, secondary, success, danger, warning, info, light, dark, link | Changes a UI Element's appearance. The allowed values are based on Bootstrap's variant CSS classes.<br><br>For React Labels, this will turn the label into an "Alert" component, with a background and text colour matching the variant. Useful for callouts, notes and static warnings ("Clicking OK will delete all your data"). |

[Tagged values for all model elements including UI component types](../tagged-values)

