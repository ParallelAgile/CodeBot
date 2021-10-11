---
layout: page
title: Generated REST API
permalink: /codebot-reference/rest-api
parent: CodeBot Reference
nav_order: 6
---

# Reference - Generated REST API

CodeBot generates a REST API from your domain model; each domain class is turned into one set of API endpoints, chiefly Create, Read, Update, Delete (CRUD) operations.

If you have multiple developers or teams each working with their own domain model, their respective REST APIs can be deployed as microservices, and made to "talk" to each other very easily by defining additional [Interfaces](../../codegen-process-guide/system-integration/crud-rest-apis) for each API.

While the following details specify what gets generated, we highly recommend that you try generating an application, then loading the OpenAPI/Swagger documentation. This will provide a far more detailed view.


## Determining which classes get an API

Only concrete, top-level classes have an API generated. (By top-level, we mean a class that isn't contained or nested as a sub-object within another class, via Composition).


## API paths

If you run the API on localhost, the server will start listening on the following URL:

```http
http://localhost:7000/username/projectCode/domainClass
```

e.g. if your CodeBot username is `acme`, project code is `tnt`, then for domain class `Customer` the URL will be:

```http
http://localhost:7000/acme/tnt/Customer
```



## API operations

For all data input operations, the incoming domain objects are validated against the generated JSON schema.

The following endpoints are generated for each domain class. The Path is appended to the above specified URL.

| HTTP method | Path     | Operation                    | Notes                       |
| ----------- | -------- | ---------------------------- | --------------------------- |
| `POST`      | `/register` | **Register**  | Creates a new user/account (identity class). |
| `POST`      | `/login` | **Login**  | If the credentials are correct, the response body includes a new JWT token. |
| `POST`      | `/`      | **Create** one or more items | Upload a single JSON object in the POST body, or an array of JSON objects. |
| `PUT`       | `/{id}`  | **Replace** an item           | Upload a single JSON object containing all an object's attributes. The ID in the path is the item ID to replace. |
| `PATCH`     | `/{id}`  | **Update** an item          | Upload a single JSON object containing individual attributes to "patch" into the target item. The ID in the path is the item ID to update. If an attribute is an array, you'll need to include *all* the array elements. |
| `GET`       | `?a1=v1&a2=v2&...` | **Read** matching items | Returns all items in this domain class' table/collection that match the "attribute name=value" query params.  |
| `POST`       | `/find` | **Read** matching items     | Returns all items in this domain class' table/collection that match a query sent in the request body. (See the Queries section below).  |
| `GET`       | `/count` | **Count all** items         | Returns the total number of items in this domain class' table/collection |
| `POST`      | `/count` | **Count** matching items    | Returns the total number of items in this domain class' table/collection that match the query in the request body. (See the Queries section below). |
| `DELETE`    | `/{id}`  | **Delete** an item          |  |
| `DELETE`    | `?a1=v1&a2=v2&...`  | **Delete** matching items | If no query-params are supplied then **all** records in the table are deleted.  |


## Additional query parameters

The **Read** and **Find** operations also support the following query parameters:

| Name   | Value example  | Notes    |
| ------ | ------ | -------- |
| _limit | `30` | Passed into the database query to limit the size of the result-set returned. Must be a positive integer, smaller than the maximum limit defined in the generated API.  |
| _sort  | `title 1` | Sorts the result-set by one or more attributes, each of which can be ascending or descending. |

### `_limit` query parameter

Must be a positive integer, smaller than the maximum limit defined in the generated API.

For example:

```http
http://localhost:7000/acme/tnt/Customer?_limit=100
```


### `_sort` query parameter

You can specify one or more attributes, separated by commas. For each "clause", specify the attribute name in `snake_case` (all lower-case), then the direction (`1` or `-1`) following a space.

Each of these is valid:

| Sort by... | Notes  |
| ---------- | ------ |
| `title`      | Sort by `title` attribute, ascending (the default direction) |
| `title 1`      | Sort by `title` attribute, ascending |
| `title -1`      | Sort by `title` attribute, descending |
| `last_name, first_name -1` | Sort by `last_name` followed by first_name |

_sort and _limit can be combined, for example, to return the latest order that's been placed:

```http
http://localhost:7000/acme/tnt/Order?_limit=1&_sort=id -1
```

(The space, of course, gets URL-encoded).

> The above query will work with MongoDB as the ObjectId is designed to be sortable, in order of time created. However if you switch to a different back-end database, please be aware that IDs in the new DB may not have the same property. In this case, we would recommend some other approach such as an auto-incrementing count.


## Queries

The **Find** and **Count** operations support name-value matching, via a JSON object supplied in the POST request body; e.g:

Let's say we're querying a `User` collection (assuming our own logged-in user belongs to the required **Admin** role):

To find all users:

```json
{
}
```

To find all users with a last_name of "Smith":

```json
{
  "last_name": "Smith"
}
```

Or:

```json
{
  "last_name": {
    "eq": "Smith"
  }
}
```

To find all users with a last_name of "Smith", but NOT a first_name of "John":

```json
{
  "last_name": {
    "eq": "Smith"
  },
  "first_name": {
    "ne": "John"
  }
}
```

To find all users aged between 18 and 30 inclusive, with a "beverage" matching an item in the array:

```json
{
  "age": {
    "gte": 18,
    "lte": 30
  },
  "beverage": {
    "in": ["CocaCola", "Pimms", "Heineken", "Water"]
  }
}
```

The queries are converted into a MongoDB-equivalent query. As we add support for more databases, the above query format will similarly be mapped to each new database.

A number of "comparators" (eq, in etc) are supported, as follows:

| Comparator | Notes  |
| ---------- | ------ |
| `eq`       | Equals |
| `ne`       | Not equal to |
| `lt`       | Less than |
| `gt`       | Greater than |
| `lte`      | Less than or equal to |
| `gte`      | Greater than or equal to |
| `in`       | Value matches one of the items in an array |
