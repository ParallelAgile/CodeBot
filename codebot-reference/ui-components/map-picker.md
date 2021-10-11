---
layout: page
title: Map Picker
permalink: /codebot-reference/ui-components/map-picker
parent: UI Component Reference
grand_parent: CodeBot Reference
nav_order: 9
---

# UI Component Reference: Map Picker

A map picker can be used as a form input component, to choose a single 'latitude, longitude' value; or as a simple location chooser; other components can then listen for a UI event via the `bind` tag or a dependency arrow. The map can be populated with map markers, each of which is a domain item loaded via the `domain` tag or by linking the map to a domain class with a Dependency arrow. In this case, the UI selection event will be a `domain object selected` event, much like a table or listbox.

## Which wireframe component?

Depending which modeling tool you're using, add the following component from the palette into the wireframe:

| Tool    |  Wireframe component(s) |
| ------- |  ---------------------- |
| Enterprise Architect | MapPicker |
| Magic Draw | MapPicker |


## Capabilities

|        |  Notes               |
| ------ |  ------------------- |
| Domain item chooser | The component can be used as an item selector, to choose a domain object. Can be used in a form, or simply to generate an 'item chosen' event. |
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
| `css class`  | Any CSS class name, without a preceding `.` | Adds the specified CSS class (or classes) to the UI element. If you define a class in a custom CSS file, you can apply it to a component using this tag. CodeBot will also recognise any 'standard' Bootstrap CSS classes such as `h1`, `h2` etc; their defined behaviour will be carried over to any future UI platforms that CodeBot generates. |
| `variant css class`  |  |  |
| `cell css class`  |  |  |
| `variant`<br>&nbsp;or:<br>&nbsp;`appearance`  | Must be one of: primary, secondary, success, danger, warning, info, light, dark, link | Changes a UI Element's appearance. The allowed values are based on Bootstrap's variant CSS classes.<br><br>For React Labels, this will turn the label into an "Alert" component, with a background and text colour matching the variant. Useful for callouts, notes and static warnings ("Clicking OK will delete all your data"). |
| `single selection`<br>&nbsp;or:<br>&nbsp;`single`  | true or false DEFAULT: `true` if in a form, otherwise `false`. | If `true`, this is a map picker where you select a single location. |
| `popup message`  |  | An optional message to display in a popup when you click the map selection marker. |
| `origin`  | `latitude,longitude` string with no spaces, e.g. `25.07037114164013,-77.39571860092475` DEFAULT: `51.505,-0.09` (Central London) | The map’s initial location, if no other location is given (e.g. data-linked, or reacting to the value in a bound component). |
| `zoom`  |  DEFAULT: `12` | The initial zoom level. |
| `width`  | any valid CSS size e.g. `50%`, `150px` | Leaflet needs the component size to be set when it’s created, so `width` and `height` tags are provided to enable that. |
| `height`  | any valid CSS size |  |
| `marker location attribute`<br>&nbsp;or:<br>&nbsp;`marker location attr`  | domain attribute name, e.g. `store location` DEFAULT: `location` | The map can be linked to a domain class to display multiple map markers. This tag defines the attribute on the linked domain class containing the `latitude,longitude` string value. For each domain object, the marker will be placed at this location. |
| `tile layer`  | A URL that follows Leaflet's [tile URL format](https://leafletjs.com/reference-1.7.1.html#tilelayer) DEFAULT: An openstreetmap layer | In addition to 'everyday' street maps, Leaflet can be extended with third-party tile layers, e.g. satellite or ESRI topological views. This tag allows you to specify the main tile layer for the map.To choose a tile layer, we recommend [this resource](https://leaflet-extras.github.io/leaflet-providers/preview/). |
| `tile attribution`  |  DEFAULT: openstreetmap attribution | Attribution text that accompanies the tile layer. This text appears at the bottom-right of the map. |
| `scroll wheel zoom`  | true or false | Whether the map can be zoomed in or out with the mouse scroll-wheel. |

[Tagged values for all model elements including UI component types](../tagged-values)

## Also see

* [To bind the map to a component, and vice versa (reference)](../ui-component-binding)
* [State-bound components (tutorial)](../../codegen-process-guide/ux/state-bound-components)

