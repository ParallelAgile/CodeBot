---
layout: page
title: UI Component Binding
permalink: /codebot-reference/ui-component-binding
parent: CodeBot Reference
nav_order: 5
---

# Reference - UI Component Binding

A component can "listen" to change events in another component, and be updated accordingly; e.g. a Media Player could listen to a listbox of Video domain items, and update to play the selected video.

For React, CodeBot generates Redux code to track and maintain global state across the app, so that components on different pages can be bound to other components' UI state.

When its value changes, a component may behave slightly differently inside a form. In a form, it'll trigger a "form value changed" event rather than an individual "component value changed" event; this is to prevent the page being slowed down with fine-grained change events flying around.

However, if another component is specifically bound to a component inside a form, it should still generate an individual "component value changed" event for the listener... so in practical terms, you may not notice a difference.
