For access to `/api/v2/microsite` you must be [Authenticated](https://github.com/bkon-connect/phy-api-docs/wiki/Authentication).

### Summary / Overview

A MicroSite is a 'mini website' that users can create and bind to a `Destination`.  They give users the ability to quickly and easily host their own content, as opposed to spinning up a new website or updating an old one.

The conceptual process of creating a MicroSite and using it (via API) is as follows:

1) Create a site via the `POST` interaction as specified below in the document

2) Use the resulting `id` in the url `phy.net/ms/:id` in your destination's `url` property.

For a detailed look at MicroSite Content Objects, see the [MicroSite Content Wiki](https://github.com/bkon-connect/phy-api-docs/wiki/MicroSite-Content)

### GET `/api/v2/microsites`

The index endpoint returns all microsites for a given account.  An example payload:

```
[
  {
    "_id": "586697ba8f4aa348a5740c5c",
    "description": "First awesome Microsite",
    "name": "1st Page",
    "ownerType": "Destination",
    "title": "Microsite Title",
    "owners": [
      "570e84ef0b37ab737ca13e3a"
    ],
    "content": [
      "586697ba8f4aa348a5740c5d",
      "586697ba8f4aa348a5740c5f"
    ]
  }
]
```

### GET `/api/v2/microsites/:id`

Fetch a specific `microsite` resource.  Requires a valid `microsite` id.

Example response:

```
{
  "_id": "586697ba8f4aa348a5740c5c",
  "description": "First awesome Microsite",
  "name": "1st Page",
  "ownerType": "Destination",
  "title": "Microsite Title",
  "owners": [
    {
      "_id": "570e84ef0b37ab737ca13e3a",
      "createdAt": "2016-04-13T17:42:07.383Z",
      "createdBy": 562,
      "account": 509,
      "notes": "",
      "url": "http://www.dollargeneral.com/category/index.jsp?categoryId=15452376",
      "__v": 0,
      "proximity": 2,
      "metaMessageActive": false,
      "name": "Seasonal Discounts"
    }
  ],
  "content": [
    {
      "_id": "586697ba8f4aa348a5740c5d",
      "updatedAt": "2016-12-30T17:22:02.000Z",
      "createdAt": "2016-12-30T17:22:02.000Z",
      "contentType": "Header",
      "body": "1st Header",
      "__v": 0
    },
    {
      "_id": "586697ba8f4aa348a5740c5f",
      "updatedAt": "2016-12-30T17:22:02.000Z",
      "createdAt": "2016-12-30T17:22:02.000Z",
      "contentType": "Content",
      "body": [
        {
          "_id": "586697ba8f4aa348a5740c5e",
          "updatedAt": "2016-12-30T17:22:02.000Z",
          "createdAt": "2016-12-30T17:22:02.000Z",
          "contentType": "Paragraph",
          "body": "1st Paragraph",
          "__v": 0
        }
      ],
      "__v": 0
    }
  ]
}
```

### POST `/api/v2/microsites`

Create a new `microsite` resource.  Valid parameters are:

<table>
  <tr>
    <th>Parameter</th>
    <th>Example</th>
    <th>Notes</th>
  </tr>
  <tr>
    <td>content</td>
    <td>`[`<br>  `{contentType: 'Paragraph', body: 'Hello Paragraph'},`<br>  `{contentType: 'Header', body: 'Hello Header'}`<br>`]`</td>
    <td>Array of Microsite Content Objects - see [MicroSite Content Wiki](https://github.com/bkon-connect/phy-api-docs/wiki/MicroSite-Content) for more</td>
  </tr>
  <tr>
    <td>faviconUrl</td>
    <td>"https://url.to.some.favicon"</td>
    <td>String - Link to a favicon image</td>
  </tr>
  <tr>
    <td>description</td>
    <td>"1st page ever"</td>
    <td>String - description of the page for usage.</td>
  </tr>
  <tr>
    <td>name</td>
    <td>"1st page"</td>
    <td>String - name of the page.  Required</td>
  </tr>
  <tr>
    <td>owners</td>
    <td>`['idOfOwner']`</td>
    <td>Array of Ref Ids - reference IDs to owners of the MicroSite.  Like meta messages, this is to account for bulk ownership / usage of a microsite. Required.</td>
  </tr>
  <tr>
    <td>ownerType</td>
    <td>"Destination"</td>
    <td>String - type of owner.  can be "Destination", "Beacon", "Event".  Required.</td>
  </tr>
  <tr>
    <td>title</td>
    <td>"Title of the Page"</td>
    <td>String - the actual title tag content of the microsite.  Required.</td>
  </tr>
</table>

example request:

```
{
  "microsite": {
    "content": [
      {"contentType":"Header", "body": "1st Header"},
      {
        "contentType":"Content",
        "body": [
          {"contentType":"Paragraph", "body": "1st Paragraph"}
        ]
      }
    ],
    "description": "First awesome Microsite",
    "name": "1st Page",
    "owners": ["570e84ef0b37ab737ca13e3a"],
    "ownerType": "Destination",
    "title": "Microsite Title"
  }
}
```

example response:

```
{
  "__v": 0,
  "updatedAt": "2016-12-30T17:22:02.000Z",
  "createdAt": "2016-12-30T17:22:02.000Z",
  "description": "First awesome Microsite",
  "name": "1st Page",
  "ownerType": "Destination",
  "title": "Microsite Title",
  "account": {
    "_id": 509,
    "owner": 562,
    "name": "Dan Demo's Account",
    "email": "testing.demo@phy.net",
    "__v": 0,
    "timezone": "",
    "defaultUrl": "",
    "customer": "cus_9RTHGGZPJheOGd",
    "notify": false,
    "subscription": "ADVANCED",
    "beta": true,
    "apiKeys": []
  },
  "_id": "586697ba8f4aa348a5740c5c",
  "owners": [
    "570e84ef0b37ab737ca13e3a"
  ],
  "content": [
    "586697ba8f4aa348a5740c5d",
    "586697ba8f4aa348a5740c5f"
  ]
}
```

### PATCH `/api/v2/microsites/:id`

Completely replace the content on an existing `microsite` resource with this `PATCH` action Requires a valid `microsite` id. Valid parameters are:

<table>
  <tr>
    <th>Parameter</th>
    <th>Example</th>
    <th>Notes</th>
  </tr>
  <tr>
    <td>content</td>
    <td>`[`<br> ` {contentType: 'Paragraph', body: 'Hello Paragraph'},`<br>  `{contentType: 'Header', body: 'Hello Header'}`<br>`]`</td>
    <td>Array of Microsite Content Objects - see Microsite Content wiki for more</td>
  </tr>
  <tr>
    <td>faviconUrl</td>
    <td>"https://url.to.some.favicon"</td>
    <td>String - Link to a favicon image</td>
  </tr>
  <tr>
    <td>description</td>
    <td>"1st page ever"</td>
    <td>String - description of the page for usage.</td>
  </tr>
  <tr>
    <td>name</td>
    <td>"1st page"</td>
    <td>String - name of the page.  Required</td>
  </tr>
  <tr>
    <td>owners</td>
    <td>`['idOfOwner']`</td>
    <td>Array of Ref Ids - reference IDs to owners of the microsite.  Like meta messages, this is to account for bulk ownership / usage of a microsite. Required.</td>
  </tr>
  <tr>
    <td>ownerType</td>
    <td>"Destination"</td>
    <td>String - type of owner. Can be "Destination", "Beacon", "Event".  Required.</td>
  </tr>
  <tr>
    <td>title</td>
    <td>"Title of the Page"</td>
    <td>String - the actual title tag content of the microsite.  Required.</td>
  </tr>
</table>

example request:

```
{
    "content":[
      {"contentType":"Header", "body":"Updated content"}
    ],
    "title": "Updated Microsite Title"
}
```

example response:

```
{
  "_id": "586697ba8f4aa348a5740c5c",
  "updatedAt": "2016-12-30T18:24:19.653Z",
  "createdAt": "2016-12-30T17:22:02.000Z",
  "description": "First awesome Microsite",
  "name": "1st Page",
  "ownerType": "Destination",
  "title": "Updated Microsite Title",
  "account": {
    "_id": 509,
    "owner": 562,
    "name": "Dan Demo's Account",
    "email": "testing.demo@phy.net",
    "__v": 0,
    "timezone": "",
    "defaultUrl": "",
    "customer": "cus_9RTHGGZPJheOGd",
    "notify": false,
    "subscription": "ADVANCED",
    "beta": true,
    "apiKeys": []
  },
  "__v": 1,
  "owners": [
    "570e84ef0b37ab737ca13e3a"
  ],
  "content": [
    "5866a6538f4aa348a5740c6c"
  ]
}
```

### DELETE `/api/v2/microsites/:id`

Remove a `microsite`.  Requires a valid `microsite` id.

Reponse is 204 with no other data.

Note: removing a microsite does not delete associated templates or themes since they may be bound to other microsites.
