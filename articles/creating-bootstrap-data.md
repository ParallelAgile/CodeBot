---
layout: page
title: Creating Bootstrap Data
permalink: /articles/creating-bootstrap-data
parent: Articles
nav_order: 4
---

# Creating Bootstrap Data

Whether a project is trivial or non-trivial, the likelihood is that it'll require bootstrap data of some sort... That is, data which already exists in the database when the application is first used.

Examples include a list of countries with country codes, currency info, metadata, etc.

In this article we'll look at the various options we considered (and tested) to create the "Video List" bootstrap data for our Hello CodeBot example.

Each approach has its own strengths and weaknesses, which we'll outline here.

## Hello CodeBot

Hello CodeBot is our simple "hello world" project; its purpose is to allow new users to quickly get something up and running using CodeBot.

Although it's about as basic as a "useful" application can get, it still touches on UI design, REST API creation, database access, user registration and authentication, and - here's the kicker - providing a list of videos to watch once you've logged in.

The video list is retrieved from MongoDB. In theory this is nice and straightforward, but the data has to come from somewhere. In other words, we needed a way to "bootstrap" the Video collection with some initial data.

## Option 1: "On Read Many" event

> The idea with this option was really a "hack", so we quickly decided against this approach. However, we present it here as the approach could be viable for other use cases.

For this approach, we defined an operation on the Video class called `on read many`. (Can also be called `onReadMany`, the name is normalised before it's generated).

> `onReadMany` is a custom event handler. It's run during the "read many" REST API call.

Our custom operation contains the following code:

```JavaScript
(wrappedData) => {
  if (wrappedData.items.length === 0) {
    wrappedData.items = [
      {
        id: "1",
        name: "Generating complete web apps including UI and database",
        url: "https://youtu.be/ZUm6esxrua8"
      },
      {
        id: "2",
        name: "Domain Driven Database Design",
        url: "https://youtu.be/zsfj64Wmdek"
      }
    ];
  }
}
```

This code is run *after* the "read" database query has been run, and `wrappedData.items` contains an array of Video records retrieved from Mongo - of course, we expect this array to be empty.

The code replaces the empty array with a new array containing two Video objects. This "fake" data will then be returned in the response.

This approach is a "quick win", but as you can imagine, it could soon become problematic as more functionality is added. The issue is that it's "pretending" that some data exists when the database is actually empty. In practice this may not be a problem at all, but could lead to some odd behaviour if some part of the application expects the "fake" records to exist in the database.

For example, if you took the above `id: "1"` or `id: "2"` and tried a GET call on the REST API, of course the IDs wouldn't be found.

So we move to the next option...


## Option 2: UI navigation state "on entry" event

## Option 3: "On Start" event

> A current downside of this option is that "on start" isn't yet supported with CodeBot hosting. This feature is on its way very soon though!

For this option, we put the following code into a custom Operation, `Video.onStart`:

```JavaScript
() => {
    const data = [
        {
            name: "Generating complete web apps including UI and database",
            url: "https://youtu.be/ZUm6esxrua8"
        },
        {
            name: "Generating complete web apps including UI and database",
            url: "https://youtu.be/ZUm6esxrua8"
        }
    ]

    const createData = () => {
        VideoDao.create(
            data,

            failed => {
                console.error("Unable to create Video bootstrap data", failed)
            },
            createError => {
                console.error("Query error creating Video bootstrap data", createError)
            },
            result => {
                console.log("Video bootstrap data created.", result)
            }
        )
    }


    VideoDao.countAll(
        failed => {
            console.error("Unable to count Video records", failed)
        },
        queryError => {
            console.error("Query error counting Video records", queryError)
        },
        count => {
            if (count === 0) {
                createData()
            }
        })
}
```

This is a fairly sizeable chunk of code, but it illustrates how to include error handling in custom event handlers.

The code first checks whether the Video collection has any data, then creates the two "bootstrap" records.


## Option 4: "On Register" event

This option could be used if the bootstrap data is actually tied to a specific user -- in other words, when a user signs up, you want to create some additional user data in a different collection.

The data could be connected to the User record via aggregation.

Another example usage would be if you have a list of "favourite" videos, and you want to populate an array of Video IDs in the User record.

But let's say you just want to run the "option 3" video creation code in the User's `onRegister` event handler. Option 3 would be the recommended way to do this, but just to illustrate, you could copy & paste the above `Video.onStart` code into an Operation `User.onRegister`.

The only required change would be to include the following line at the top of `User.onRegister`:

```JavaScript
(user) => {
    const VideoDao = require("../database/VideoDao.js")

    ... etc ...
```

In fact, this technique can be used if you want to also create bootstrap data in other collections related to the newly registered user.
