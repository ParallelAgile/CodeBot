---
layout: page
title: Hosting
permalink: /codegen-process-guide/getting-started/hosting
parent: Getting Started
grand_parent: CodeBot Guide
nav_order: 3
---

# Hosting

PA offers a managed hosting service on AWS, for generated databases, APIs and web-apps. The hosting is suitable for rapid prototyping, setting up a quick demo, and for production systems.

When configured to do so, CodeBot will deploy the generated app straight to the cloud as part of its code generation process, making the whole thing very convenient and easy to use.

Essentially, three things are hosted:

1. MongoDB database (this is stored securely and privately in AWS' DocumentDB database)
2. REST API
3. React web-app

The React app is generated as a Single-Page Application (SPA) based on create-react-app. For hosting, CodeBot builds the SPA using AWS CodeBuild, and deploys it to S3 (with reverse-proxying done by CloudFront).


## Hosted REST API URLs

Your hosted API will have a URL along these lines:

`https://parallelagile.net/hosted/username/project`

`username` is your username, entirely lower-cased. Similarly, `project` is your **project code**, lower-cased.

For example, if your username is "fred" and you've published a project called "Hockey Scores" (with a project code "hockey"):

`https://parallelagile.net/hosted/fred/hockey`

If you're using the default project (i.e. the one that gets created automatically when you sign up), the URL would be:

`https://parallelagile.net/hosted/fred/default`


The project code can be changed if needed -- the [Web Console](web-console) page shows how.


## Hosted UI URLs

URLs for hosted UIs follow a similar pattern to hosted APIs:

`https://parallelagile.net/ui/hosted/username/project`

i.e. it's identical except for the "ui/" part.



> **[> Next: Hello Codebot project](../hello-codebot-project)**
