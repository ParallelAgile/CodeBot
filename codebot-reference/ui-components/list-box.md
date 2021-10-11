---
layout: page
title: List Box
permalink: /codebot-reference/ui-components/list-box
parent: UI Component Reference
grand_parent: CodeBot Reference
nav_order: 8
---

# UI Component Reference: List Box

A listbox can be linked to a domain class (via the `domain` tag or a Dependency arrow), to display data from the domain class' relevant API endpoint. Each row shows a single attribute. The selected value is always the domain object's `id` attribute, though UI listeners are given the whole domain object. A listbox can also be linked to an Enumeration, in which case it will display 'hardwired' enum values. The selected value is then the enum name.

## Which wireframe component?

Depending which modeling tool you're using, add the following component from the palette into the wireframe:

| Tool    |  Wireframe component(s) |
| ------- |  ---------------------- |
| Enterprise Architect | List |
| Magic Draw | List |


## Capabilities

|        |  Notes               |
| ------ |  ------------------- |
| Domain item chooser | The component can be used as an item selector, to choose a domain object. Can be used in a form, or simply to generate an 'item chosen' event. |
| Enum chooser | The component can be used to choose from an array of Enumeration values. Can be used in a form, or simply to generate an 'item chosen' event. |
| Multi selection | Multiple items can be chosen. To enable, add a tagged value `multi selection` with the value `true`. |
| Domain data | The component can be linked to a domain class, via the `domain` tag or a dependency arrow. The component will show data loaded from the domain class' relevant API endpoint. |
| Bind target | Other components can listen and react to this component's' UI events, via their `bind` tag or a dependency arrow pointing to this component. |

## Filtering the list

If you want to filter the items that appear in the list, add a tagged value called `filter`. This can include a JavaScript/TypeScript predicate.

Three values are available to the predicate:

1. the domain item (one of the rows in the list); the name will be the domain class name as "lowerCamelCase", e.g. `video` or `videoReview`
2. `index` - the position of this item in the (unfiltered) list, zero-indexed
3. an array of the whole list, named e.g. `videoItems` or `videoReviewItems`

The predicate *must* be a valid JavaScriptor TypeScript expression, and must resolve to boolean. If not, the whole React build might break, so tread carefully!

> We recommend writing the predicate first in the generated React code and testing it, before copying it into the model.

Example predicates:

```JavaScript
video.url.startsWith("https://")
```

```JavaScript
video.name.length > 0
```

```JavaScript
index % 2 === 1
```

Or to truncate the list to the first 20 items:
```JavaScript
index < 20
```

The same `filter` tag is also available on other data-linked components - [ComboBox](combo-box), [Table](table), [Map](map-picker).


## Tagged values

| Tag      | Allowed values | Notes               |
| -------- | -------------- | ------------------- |
| `domain`  |  | Links a component to a domain class, and optionally an attribute.<br><br>Depending on the component, it will then use the domain data in some way, e.g. to populate a table or listbox with domain data for selection.<br><br>The linked data will be loaded via the domain class' matching REST API endpoint, with loading state managed in the UI via a Redux domain selector.<br><br>Please note: This tag is the same as connecting the element to a domain class with a Dependency arrow. |
| `display domain`  |  | Specifies which domain class attribute to display.  For cases where the display attribute/relationship is different from the 'data' domain attribute/relationship. |
| `form domain`  |  | For Domain Chooser UI Elements (listbox, ComboBox), where the form attribute/relationship is different from the 'data' domain attribute/relationship, as two domain classes are involved. |
| `css class`  | Any CSS class name, without a preceding `.` | Adds the specified CSS class (or classes) to the UI element. If you define a class in a custom CSS file, you can apply it to a component using this tag. CodeBot will also recognise any 'standard' Bootstrap CSS classes such as `h1`, `h2` etc; their defined behaviour will be carried over to any future UI platforms that CodeBot generates. |
| `variant css class`  |  |  |
| `cell css class`  |  |  |
| `variant`<br>&nbsp;or:<br>&nbsp;`appearance`  | Must be one of: primary, secondary, success, danger, warning, info, light, dark, link | Changes a UI Element's appearance. The allowed values are based on Bootstrap's variant CSS classes.<br><br>For React Labels, this will turn the label into an "Alert" component, with a background and text colour matching the variant. Useful for callouts, notes and static warnings ("Clicking OK will delete all your data"). |
| `multi selection`<br>&nbsp;or:<br>&nbsp;`multiple selection`, <br>&nbsp;`multi`  | true or false DEFAULT: `false` | If `true`, multiple items can be selected; if 'false', it's single-selection only. |

[Tagged values for all model elements including UI component types](../tagged-values)

