---
layout: page
title: Tagged Values
permalink: /codebot-reference/tagged-values
parent: CodeBot Reference
nav_order: 3
---

# Reference - Tagged Values

A note about tag names:
Throughout this guide you'll see tag names in "lower sentence case", e.g. `stylesheet url`. Although we recommend using this style, you can use upper case in places if preferred, or underscores, full-stops/periods and dashes in place of spaces; e.g. `Stylesheet URL` or `StyleSheet_URL` would also work. The names are all "normalised" by CodeBot before they're used.


## Variant

The `variant` tag is applicable to some UI components, primarily `Label`, `Table` and containers (`Panel`/`Client Area`). The allowed values are based on Bootstrap's variant CSS classes, as follows:

![Variants](../images/bootstrap-variants.png "Variants")





## Image component

Some of these tags are based on Bootstrap values. For more info: https://react-bootstrap.github.io/components/images/

| Tag      | Values                                            | Notes              |
| ---------| ------------------------------------------------- | ------------------ |
| `url`    | `https://example.com/image.png`                   | A static URL containing an image, must be reachable by any browser using the generated web-app |
| `shape`  | One of: `rounded`, `roundedCircle`, `thumnbnail`  | Affects the image appearance |
| `fluid`  | `true` (default) or `false`                       | Scales the image nicely to the parent element |


## Table component

Some of these tags are based on Bootstrap values. For more info: https://react-bootstrap.github.io/components/table/

| Tag      | Values                                            | Notes              |
| ---------| ------------------------------------------------- | ------------------ |
| `size`   | `sm`                    | Cuts the table row spacing in half |
