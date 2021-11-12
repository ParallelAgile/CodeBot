---
layout: page
title: Password Field
permalink: /codebot-reference/ui-components/password-field
parent: UI Component Reference
grand_parent: CodeBot Reference
nav_order: 11
---

# UI Component Reference: Password Field

'Masked' text input, for entering passwords or other sensitive data. To create using EA, add a *Text Field* component and then give it a stereotype of `<<WireframePassword>>`. Using MagicDraw, either do the same or add a *Password Field* component. In either case, if the linked domain attribute is called 'password', the component will automatically be a PasswordField.

## Which wireframe component?

Depending which modeling tool you're using, add the following component from the palette into the wireframe:

| Tool    |  Wireframe component(s) |
| ------- |  ---------------------- |
| Enterprise Architect | Text Field |
| Magic Draw | Password Field, Text Field |


## Capabilities

|        |  Notes               |
| ------ |  ------------------- |
| Single value input | The component allows a single value to be input. |
| Domain data | The component can be linked to a domain class, via the `domain` tag or a dependency arrow. The component will show data loaded from the domain class' relevant API endpoint. |
| Bind target | Other components can listen and react to this component's' UI events, via their `bind` tag or a dependency arrow pointing to this component. |


## Tagged values

| Tag      | Allowed values | Notes               |
| -------- | -------------- | ------------------- |
| `domain`  |  | Links a component to a domain class, and optionally an attribute.<br><br>Depending on the component, it will then use the domain data in some way, e.g. to populate a table or listbox with domain data for selection.<br><br>The linked data will be loaded via the domain class' matching REST API endpoint, with loading state managed in the UI via a Redux domain selector.<br><br>Please note: This tag is the same as connecting the element to a domain class with a Dependency arrow. |
| `display domain`  |  | Specifies which domain class attribute to display.  For cases where the display attribute/relationship is different from the 'data' domain attribute/relationship. |
| `form domain`  |  | For Domain Chooser UI Elements (listbox, ComboBox), where the form attribute/relationship is different from the 'data' domain attribute/relationship, as two domain classes are involved. |
| `filter`  |  | Define a single-line predicate (valid TypeScript expression that evaluates to a boolean) to filter a UI list. |
| `placeholder`  |  | For text input, the 'placeholder' text to display when the textfield is empty. |
| `css class`  | Any CSS class name, without a preceding `.` | Adds the specified CSS class (or classes) to the UI element. If you define a class in a custom CSS file, you can apply it to a component using this tag. CodeBot will also recognise any 'standard' Bootstrap CSS classes such as `h1`, `h2` etc; their defined behaviour will be carried over to any future UI platforms that CodeBot generates. |
| `variant css class`  |  |  |
| `cell css class`  |  |  |
| `default value`<br>&nbsp;or:<br>&nbsp;`default`  |  |  |
| `variant`<br>&nbsp;or:<br>&nbsp;`appearance`  | Must be one of: primary, secondary, success, danger, warning, info, light, dark, link | Changes a UI Element's appearance. The allowed values are based on Bootstrap's variant CSS classes.<br><br>For React Labels, this will turn the label into an "Alert" component, with a background and text colour matching the variant. Useful for callouts, notes and static warnings ("Clicking OK will delete all your data"). |

[Tagged values for all model elements including UI component types](../tagged-values)

