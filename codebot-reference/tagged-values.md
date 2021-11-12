---
layout: page
title: Tagged Values
permalink: /codebot-reference/tagged-values
parent: CodeBot Reference
nav_order: 3
---

# Reference - Tagged Values

This page contains all the tagged values that CodeBot recognises. Tag names generally are used consistently in all UI components and elsewhere,
so you should find pretty quickly that you start to recognise their names and purposes, and "intuitively know" which tag name to use.

## Tags by Category

The tags are grouped here by their general category:

### Any element

Applicable to any model element.

| Tag      | Allowed values   | Notes               |
| ---------| ---------------- | ------------------- |
| `plural`  | true or false | In certain cases, CodeBot will 'pluralise' an element's name, following basic 'Anglified' rules such as adding an s, or turning y into ies. To override the pluralised name, add this tagged value to the model element. |

### DAO Interfaces

These tags are used on Interfaces that represent a Data Access Object such as an external REST API.

| Tag      | Allowed values   | Notes               |
| ---------| ---------------- | ------------------- |
| `default operations`<br>&nbsp;or:<br>&nbsp;`default ops`, <br>&nbsp;`defaults`  | Multiple values are allowed, but each must be one of: count, create, delete file, delete many, delete one, download file, find many, find one, get many, login, read one, register, replace, replace file, update, upload file | Specifies the default CRUD operations that CodeBot should generate on the DAO interface pointed to by this domain class. Please note: This tag is placed on the class or dependency pointing to the Interface, not the interface itself. |
| `path`  |  | For external REST APIs, an additional path that is appended to the base URL for operations. |
| `url`  |  | The base URL for external REST APIs. |

### Domain classes

These tags are used on domain classes.

| Tag      | Allowed values   | Notes               |
| ---------| ---------------- | ------------------- |
| `multiplicity`<br>&nbsp;or:<br>&nbsp;`multi`  |  | Specifies whether the Operation return type is a single value or an array. Use 'common' notation such as: 1, 0, or 0..* |
| `node dependency`<br>&nbsp;or:<br>&nbsp;`node dependencies`, <br>&nbsp;`node deps`  |  | Defines a Node.js library dependency, which will be added to the Application-layer JavaScript module, and to `package.json`. |

### Tasks

These tags are used on Task operations.

| Tag      | Allowed values   | Notes               |
| ---------| ---------------- | ------------------- |
| `method`  | Must be one of: GET, HEAD, POST, PUT, PATCH, DELETE, HEAD, OPTIONS | The HTTP method this operation should use when making a request to the external REST API. |


### UI Elements

These tags are used on UI Elements within a wireframe.

Some of these tags are based on Bootstrap properties and values. For more info, find the relevant matching component at: [https://react-bootstrap.github.io/components](https://react-bootstrap.github.io/components/).

| Tag      | Components | Allowed values | Notes               |
| ---------| ---------- | -------------- | ------------------- |
| `action`  | [Button](ui-components/button), [Link](ui-components/link) | Must be one of: create, replace, update, delete, get many, find, find one, login, register, logout, task, task, form task | With a form button, this tag defines the type of action that will take place when the button is clicked - essentially, which REST API endpoint to call; e.g. 'create'. |
| `bind`  | [Button](ui-components/button), [Checkbox](ui-components/checkbox), [ComboBox](ui-components/combo-box), [Image](ui-components/image), [Label](ui-components/label), [Link](ui-components/link), [MapPicker](ui-components/map-picker), [MediaPlayer](ui-components/media-player), [RangeInput](ui-components/range-input), [Table](ui-components/table), [TextArea](ui-components/text-area), [TextField](ui-components/text-field) |  | Makes this UI Element listen to another UI element for events (e.g. row item selected), via a Redux UI global state selector.<br><br>This tag is the same as connecting the elements with a Dependency arrow. However, you can use this tag, for example, if the other UI element is on a different wireframe.<br><br>The following component types can be 'state-bound' (i.e. listen to another UI Element via the bind tag or dependency arrow): <br><br>Button, Checkbox, ComboBox, Link, ListBox, MapPicker, MediaPlayer, PasswordField, RangeInput, Table, TextArea, TextField |
| `cell css class`  | [All](ui-components/) |  |  |
| `columns`<br>&nbsp;or:<br>&nbsp;`column`, <br>&nbsp;`attribute`  | [Table](ui-components/table) |  DEFAULT: All attributes except `id`. | For a data-linked table, this specifies which attributes to display as table columns. |
| `css class`  | [All](ui-components/) | Any CSS class name, without a preceding `.` | Adds the specified CSS class (or classes) to the UI element. If you define a class in a custom CSS file, you can apply it to a component using this tag. CodeBot will also recognise any 'standard' Bootstrap CSS classes such as `h1`, `h2` etc; their defined behaviour will be carried over to any future UI platforms that CodeBot generates. |
| `default value`<br>&nbsp;or:<br>&nbsp;`default`  | [Checkbox](ui-components/checkbox), [PasswordField](ui-components/password-field), [RangeInput](ui-components/range-input), [TextArea](ui-components/text-area), [TextField](ui-components/text-field) |  |  |
| `display domain`  | [Button](ui-components/button), [Checkbox](ui-components/checkbox), [ComboBox](ui-components/combo-box), [Image](ui-components/image), [Link](ui-components/link), [ListBox](ui-components/list-box), [MapPicker](ui-components/map-picker), [MediaPlayer](ui-components/media-player), [PasswordField](ui-components/password-field), [RangeInput](ui-components/range-input), [Table](ui-components/table), [TextArea](ui-components/text-area), [TextField](ui-components/text-field) |  | Specifies which domain class attribute to display.  For cases where the display attribute/relationship is different from the 'data' domain attribute/relationship. |
| `display text`<br>&nbsp;or:<br>&nbsp;`text`  | [ComboBox](ui-components/combo-box), [Label](ui-components/label), [Link](ui-components/link), [RangeInput](ui-components/range-input), [TextArea](ui-components/text-area), [TextField](ui-components/text-field) |  DEFAULT: the UI element name | Text to display, if not using the component name.<br><br>For EA wireframes the element name is normally used; however this tag will override that if the name needs to be different, e.g. to avoid duplicate element names, or if the text won't map well to variable names etc. |
| `domain`  | [Button](ui-components/button), [Checkbox](ui-components/checkbox), [ComboBox](ui-components/combo-box), [Image](ui-components/image), [Link](ui-components/link), [ListBox](ui-components/list-box), [MapPicker](ui-components/map-picker), [MediaPlayer](ui-components/media-player), [PasswordField](ui-components/password-field), [RangeInput](ui-components/range-input), [Table](ui-components/table), [TextArea](ui-components/text-area), [TextField](ui-components/text-field) |  | Links a component to a domain class, and optionally an attribute.<br><br>Depending on the component, it will then use the domain data in some way, e.g. to populate a table or listbox with domain data for selection.<br><br>The linked data will be loaded via the domain class' matching REST API endpoint, with loading state managed in the UI via a Redux domain selector.<br><br>Please note: This tag is the same as connecting the element to a domain class with a Dependency arrow. |
| `failure message`  | [Button](ui-components/button), [Link](ui-components/link) |  | Custom user-facing error message to display if the REST API returned an error. Use 'none' to prevent the message being shown at all. |
| `filter`  | [Button](ui-components/button), [Checkbox](ui-components/checkbox), [ComboBox](ui-components/combo-box), [Image](ui-components/image), [Link](ui-components/link), [ListBox](ui-components/list-box), [MapPicker](ui-components/map-picker), [MediaPlayer](ui-components/media-player), [PasswordField](ui-components/password-field), [RangeInput](ui-components/range-input), [Table](ui-components/table), [TextArea](ui-components/text-area), [TextField](ui-components/text-field) |  | Define a single-line predicate (valid TypeScript expression that evaluates to a boolean) to filter a UI list. |
| `fluid`  | [Image](ui-components/image) | true or false | If true, scales the image nicely to the parent element. |
| `form domain`  | [Button](ui-components/button), [Checkbox](ui-components/checkbox), [ComboBox](ui-components/combo-box), [Image](ui-components/image), [Link](ui-components/link), [ListBox](ui-components/list-box), [MapPicker](ui-components/map-picker), [MediaPlayer](ui-components/media-player), [PasswordField](ui-components/password-field), [RangeInput](ui-components/range-input), [Table](ui-components/table), [TextArea](ui-components/text-area), [TextField](ui-components/text-field) |  | For Domain Chooser UI Elements (listbox, ComboBox), where the form attribute/relationship is different from the 'data' domain attribute/relationship, as two domain classes are involved. |
| `height`  | [MapPicker](ui-components/map-picker) | any valid CSS size |  |
| `image url`  | [Image](ui-components/image) | `https://example.com/image.png` | A static URL or relative path pointing to an image; must be reachable by any browser using the generated web-app. |
| `justify`  | [Container](ui-components/container) | Must be one of: left, right, center | Text justification for the UI element container. |
| `marker location attribute`<br>&nbsp;or:<br>&nbsp;`marker location attr`  | [MapPicker](ui-components/map-picker) | domain attribute name, e.g. `store location` DEFAULT: `location` | The map can be linked to a domain class to display multiple map markers. This tag defines the attribute on the linked domain class containing the `latitude,longitude` string value. For each domain object, the marker will be placed at this location. |
| `multi selection`<br>&nbsp;or:<br>&nbsp;`multiple selection`, <br>&nbsp;`multi`  | [ListBox](ui-components/list-box), [Table](ui-components/table) | true or false DEFAULT: `false` | If `true`, multiple items can be selected; if 'false', it's single-selection only. |
| `origin`  | [MapPicker](ui-components/map-picker) | `latitude,longitude` string with no spaces, e.g. `25.07037114164013,-77.39571860092475` DEFAULT: `51.505,-0.09` (Central London) | The map’s initial location, if no other location is given (e.g. data-linked, or reacting to the value in a bound component). |
| `placeholder`  | [TextField](ui-components/text-field), [TextArea](ui-components/text-area), [PasswordField](ui-components/password-field) |  | For text input, the 'placeholder' text to display when the textfield is empty. |
| `popup message`  | [MapPicker](ui-components/map-picker) |  | An optional message to display in a popup when you click the map selection marker. |
| `read only`  | [ComboBox](ui-components/combo-box), [Label](ui-components/label), [Link](ui-components/link), [RangeInput](ui-components/range-input), [TextArea](ui-components/text-area), [TextField](ui-components/text-field) |  DEFAULT: no | If true (or yes), the input element can't be edited; updates are only via a bound element such as a ComboBox. |
| `scroll wheel zoom`  | [MapPicker](ui-components/map-picker) | true or false | Whether the map can be zoomed in or out with the mouse scroll-wheel. |
| `shape`  | [Image](ui-components/image) | Must be one of: rounded, roundedCircle, thumnbnail | Affects the image appearance. |
| `single selection`<br>&nbsp;or:<br>&nbsp;`single`  | [MapPicker](ui-components/map-picker) | true or false DEFAULT: `true` if in a form, otherwise `false`. | If `true`, this is a map picker where you select a single location. |
| `success message`  | [Button](ui-components/button), [Link](ui-components/link) |  | Lets you override the message displayed when an 'action' completes successfully, e.g. on form create. Use the text 'none' to prevent any message being shown ('none' is required as EA will interpret a blank tagged value as absent, i.e. won't export it). |
| `table size`  | [Table](ui-components/table) | Must be one of: sm | Cuts the table row spacing in half |
| `task operation`  | [Button](ui-components/button), [Link](ui-components/link) | Must be one of: create, replace, update, delete, get many, find, find one, login, register, logout, task, task, form task | For a 'task' action, pinpoints the domain class and Operation that the action should invoke - e.g. Game.upgradePlayer |
| `tile attribution`  | [MapPicker](ui-components/map-picker) |  DEFAULT: openstreetmap attribution | Attribution text that accompanies the tile layer. This text appears at the bottom-right of the map. |
| `tile layer`  | [MapPicker](ui-components/map-picker) | A URL that follows Leaflet's [tile URL format](https://leafletjs.com/reference-1.7.1.html#tilelayer) DEFAULT: An openstreetmap layer | In addition to 'everyday' street maps, Leaflet can be extended with third-party tile layers, e.g. satellite or ESRI topological views. This tag allows you to specify the main tile layer for the map.To choose a tile layer, we recommend [this resource](https://leaflet-extras.github.io/leaflet-providers/preview/). |
| `value type`<br>&nbsp;or:<br>&nbsp;`data type`, <br>&nbsp;`type`  | [TextField](ui-components/text-field), [TextArea](ui-components/text-area) |  | This allows input elements such as textfields to match the required data type, e.g. only allow numbers; or (on mobile) show a keyboard tailored for entering an email address; e.g. 'email', or the 'usual' attribute data types such as number, int, string. |
| `variant`<br>&nbsp;or:<br>&nbsp;`appearance`  | [All](ui-components/) | Must be one of: primary, secondary, success, danger, warning, info, light, dark, link | Changes a UI Element's appearance. The allowed values are based on Bootstrap's variant CSS classes.<br><br>For React Labels, this will turn the label into an "Alert" component, with a background and text colour matching the variant. Useful for callouts, notes and static warnings ("Clicking OK will delete all your data"). |
| `variant css class`  | [All](ui-components/) |  |  |
| `width`  | [MapPicker](ui-components/map-picker) | any valid CSS size e.g. `50%`, `150px` | Leaflet needs the component size to be set when it’s created, so `width` and `height` tags are provided to enable that. |
| `zoom`  | [MapPicker](ui-components/map-picker) | 1 to 12 DEFAULT: `12` | The initial zoom level. |

## Tag name usage

Throughout this documentation you'll see tag names in "lower sentence case", e.g. `stylesheet url`. Although we recommend using this style, you can use upper case in places if preferred, or underscores, full-stops/periods and dashes in place of spaces; e.g. `Stylesheet URL` or `StyleSheet_URL` would also work. The names are all "normalised" by CodeBot before they're used.

## A note about Variants

The `variant` tag is applicable to some UI components, primarily `Label`, `Table` and containers (`Panel`/`Client Area`). The allowed values are based on Bootstrap's variant CSS classes, as follows:

![Variants](../images/bootstrap-variants.png "Variants")

While these variants are quite Bootstrap-specific, we'll carry them over to any future UI platforms that CodeBot generates, so that the same wireframes can be reused.

