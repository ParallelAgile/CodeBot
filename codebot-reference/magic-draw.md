---
layout: page
title: MagicDraw Support
permalink: /codebot-reference/magic-draw
parent: CodeBot Reference
nav_order: 11
---


# MagicDraw Support

Most of the UML modeling and wireframing examples in this guide are based on Enterprise Architect (EA) from Sparx. However, CodeBot also provides first-class support for [MagicDraw](https://www.3ds.com/products-services/catia/products/no-magic/) (MD), with support for more modeling and UX design frameworks planned.

The guide is mostly the same regardless of which modeling tool you're using. However, inevitably there are a few differences -- where these differences occur, we show examples for both EA and MD.

Additionally, on this page we've collected MD-specific UML modeling documentation for generating full-stack applications with MagicDraw. Also refer to our [Hello CodeBot](../codegen-process-guide/hello-codebot-project) project for an MD-specific example model.

# Generate an application from a MagicDraw model

To generate an MD-based application, perform these steps:

1. Export the full model as an XMI 2.5 file (this has an "xml" file extension)
2. Log into the CodeBot [web console](https://parallelagile.net/) and choose a project
3. Click "Upload XMI", and drag in the XMI file (or select it in your local filesystem)
4. Hit "Run CodeBot"!

> The web console instructions specify XMI 2.1; however this is a requirement for exported EA models. For MD, make sure the XMI version is 2.5.

# UML Profile

In addition to the usual UML and wireframe modeling semantics, CodeBot reads UML stereotypes and tagged values. MD is stricter than EA in some cases, and requires that both stereotypes and tagged values are defined in a UML profile. (EA has strong support for UML profiles, but the requirement is optional).

We provide a [UML profile](uml-profile) which can be imported into both EA and MD. This profile adds custom stereotypes and tagged values.

# UI

## Asset files - images, CSS files etc

If the model contains embedded/attached files such as JPGs, PNGs, movies, CSS files etc, these will be available as resources in the generated web-app.

In your wireframes, you can associate components with attached images, e.g. to display a page banner or icon.

To organise the attached files, we recommend creating a package called `Assets`, and keeping all the web assets there.

To attach a file to the model:

1. Drag-and-drop the file into the `Assets` package
2. When MD prompts, choose "Create Attached File"

Alternatively, right-click the `Assets` package, choose *Create Element .. Attached File* and select the file from the local filesystem.

## Displaying an Image

To show an image (e.g. page banner), you need to associate a Label with an attached image asset:

1. Follow the above steps to attach an image to the model
2. Add a Label to the wireframe
3. Drag-and-drop the attached image from `Assets` onto the label in the wireframe. The label's *Image* property should update to show the image
4. To tell MD to display the image in the wireframe, change the label's *Icon* property to `custom`.

The same image asset can be reused by other wireframe components, e.g. to show the same banner at the top of every page.
 