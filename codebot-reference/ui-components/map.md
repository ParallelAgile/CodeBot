---
layout: page
title: Map
permalink: /codebot-reference/ui-components/map
parent: UI Component Reference
grand_parent: CodeBot Reference
nav_order: 11
---

# UI Component Reference: Map

`Map` components can be used as a "single selection" map picker (i.e. choose a location), or to show data-linked *map markers* (or as both - it's possible to pick an individual location, while also showing map markers that can be clicked on). In the latter case (with map markers), think of the map component as a kind of graphical `ListBox` - it's showing a selection of data items just like a list, where each item can generate an "item selected" event.

For React apps, CodeBot uses [React Leaflet](https://react-leaflet.js.org/), which is a React wrapper around [Leaflet](https://leafletjs.com/). The map is contained in `components/CbMap.ts` ("codebot map").

## Creating a map

To add a map to the wireframe, in EA:

1. Add an `Image` component to the wireframe
2. In the Properties panel, add a stereotype called `WireframeMap` (you may need to add it as a custom stereotype if it isn't installed in a UML profile)
3. Optionally, delete the `WireframeImage` stereotype

> In determining the component type, CodeBot will give preference to `Map` over `Image`, but you might want to delete the `WireframeImage` stereotype anyway, so it doesn't look like an image component in the wireframe.


## Using the map in a data-linked form

When configured to be a "map picker", a map can be used like any other text input control in a form. As with other components, either:

* give the map the same name as the attribute it represents, or
* use the `domain` tag to specify the attribute name

The attribute must be a `string` data type. When the user clicks the map to choose a location, the value emitted will be a single string containing its "latitude,longitude".

## Populating the map with markers

To add *map markers*, link the map to a domain class (via the `domain` tag or a Dependency arrow). The linked attribute name should be the location coordinates, in the form of a "latitude,longitude" string. Each domain item in the relevant database table/collection will then be added as a clickable marker.

When configured like this, the map will behave like a listbox. Click a marker to "choose" that domain item.


## Tagged values

The `Map` component is primarily configured through the following tagged values:

| Tag name      | Values            | Default value | Notes                          |
| ------------- | ----------------- | ------------- | ------------------------------ |
| `single selection` | `true` or `false` | In a form, default is true, otherwise false. | If true, this is a map picker where you select a single location. |
| `popup message`    | Any text |         | If this is a map picker, an optional message to display in a popup when you click the selection marker. |
| `origin`           | latitude,longitude string with no spaces, e.g. `25.07037114164013,-77.39571860092475` | `51.505,-0.09` (Central London) | The map's default location, if no other location is given (e.g. data-linked, or reacting to the value in some other component). |
| `zoom`             | Integer  | `12`         | The initial zoom level |
| `width`            | any valid CSS size e.g. `50%`, `150px`  | `50rem` | Leaflet needs the component size to be set when it's created, so width and height tags are provided to enable that. |
| `height`           | any valid CSS size      | `40rem`  | |
| `marker location attribute` | domain attribute name | `location`  | When the map is linked to a domain class (to display multiple map markers), this is the attribute on the linked domain class containing the "latitude,longitude" string value. The marker will be placed at this location. |
| `scroll wheel zoom` | `true` or `false` | `false` | Whether the map can be zoomed in or out with the mouse scroll-wheel. |
| `css class`        | Any CSS class name, without a preceding `.`  |  | |
| `tile layer`       | A URL that follows Leaflet's [tile URL format](https://leafletjs.com/reference-1.7.1.html#tilelayer) | An openstreetmap layer  | In addition to "everyday" street maps, Leaflet can be extended with third-party tile layers, e.g. satellite or topological views. This tag allows you to specify the main tile layer for the map. |
| `tile attribution` | Any text  | openstreetmap attribution | Attribution text that accompanies the tile layer. This text appears at the bottom-right of the map. |

> To choose a tile layer, we recommend [this resource](https://leaflet-extras.github.io/leaflet-providers/preview/).

[Common tagged values](../tagged-values) shared by most components.


## UI Actions Triggered

The following actions/events are triggered at run-time:

| Event       | Data type          | Created when...    | Notes    |
| ----------- | ------------------ | ------------------ | -------- |
| Domain item chosen | Domain object/item | a map marker is clicked | The map must be linked to a domain class (via `domain` tag or a Dependency arrow) |
| Value changed | string  | "single selection" map (i.e. map picker) is clicked, to choose a location | The text value is a single string containing "latitude,longitude"  |

## Receivable UI Actions

The following action/event types can be received by the map, by binding it to some other component:

| Event               | Data type          | Notes    |
| ------------------- | ------------------ | -------- |
| Domain item chosen  | Domain object/item | Moves the map to the new location. Requires a text attribute representing "latitude,longitude"; this can be specified in the `bind` tag, or (if a Dependency arrow is being used) by naming the arrow with the attribute name. |
| Value changed  | string | Moves the map to the new location. The bound value (emitted by the other component) should be a string representing "latitude,longitude". |


To bind the map to a component (and vice versa), see [UI Component Binding](../ui-component-binding) (reference) and [State-bound Components](../../codegen-process-guide/ux/state-bound-components) (tutorial).
