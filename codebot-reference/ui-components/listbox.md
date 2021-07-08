---
layout: page
title: List Box
permalink: /codebot-reference/ui-components/listbox
parent: UI Component Reference
grand_parent: CodeBot Reference
nav_order: 8
---

# UI Component Reference: List Box (item chooser)

Page will be added very soon...



## Creating a Listbox


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

The same `filter` tag is also available on other data-linked components - [ComboBox](combobox), [Table](table), [Map](map).

## Tagged values

See: [Common tagged values](../tagged-values)
