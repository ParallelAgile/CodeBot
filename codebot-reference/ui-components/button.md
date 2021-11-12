---
layout: page
title: Button
permalink: /codebot-reference/ui-components/button
parent: UI Component Reference
grand_parent: CodeBot Reference
nav_order: 1
---

# UI Component Reference: Button

If assigned an `action` tag, a button can submit a form container. A button can also be used as a navigation trigger to a different page (or other URL, like a Link component).

## Which wireframe component?

Depending which modeling tool you're using, add the following component from the palette into the wireframe:

| Tool    |  Wireframe component(s) |
| ------- |  ---------------------- |
| Enterprise Architect | Button |
| Magic Draw | Button |


## Capabilities

|        |  Notes               |
| ------ |  ------------------- |
| Navigation action | The component can trigger a "direct" navigation transition, from a UI event such as `on click`.<br>This is different from a "subsequent" navigation after, say, `on create`. |
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
| `filter`  |  | Define a single-line predicate (valid TypeScript expression that evaluates to a boolean) to filter a UI list. |
| `action`  | Must be one of: create, replace, update, delete, get many, find, find one, login, register, logout, task, task, form task | With a form button, this tag defines the type of action that will take place when the button is clicked - essentially, which REST API endpoint to call; e.g. 'create'. |
| `success message`  |  | Lets you override the message displayed when an 'action' completes successfully, e.g. on form create. Use the text 'none' to prevent any message being shown ('none' is required as EA will interpret a blank tagged value as absent, i.e. won't export it). |
| `failure message`  |  | Custom user-facing error message to display if the REST API returned an error. Use 'none' to prevent the message being shown at all. |
| `task operation`  | Must be one of: create, replace, update, delete, get many, find, find one, login, register, logout, task, task, form task | For a 'task' action, pinpoints the domain class and Operation that the action should invoke - e.g. Game.upgradePlayer |
| `css class`  | Any CSS class name, without a preceding `.` | Adds the specified CSS class (or classes) to the UI element. If you define a class in a custom CSS file, you can apply it to a component using this tag. CodeBot will also recognise any 'standard' Bootstrap CSS classes such as `h1`, `h2` etc; their defined behaviour will be carried over to any future UI platforms that CodeBot generates. |
| `variant css class`  |  |  |
| `cell css class`  |  |  |
| `variant`<br>&nbsp;or:<br>&nbsp;`appearance`  | Must be one of: primary, secondary, success, danger, warning, info, light, dark, link | Changes a UI Element's appearance. The allowed values are based on Bootstrap's variant CSS classes.<br><br>For React Labels, this will turn the label into an "Alert" component, with a background and text colour matching the variant. Useful for callouts, notes and static warnings ("Clicking OK will delete all your data"). |

[Tagged values for all model elements including UI component types](../tagged-values)

## Also see

* [Container](container)
* [Link component](link)

