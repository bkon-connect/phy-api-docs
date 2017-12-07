For access to the `/api/v2/destinations` endpoint you must be [Authenticated](https://github.com/bkon-connect/phy-api-docs/wiki/Authentication).

#### GET `/api/v2/destinations/`

The index endpoint that returns all destinations for a given user.  Example payload:

```
[
  {
    "_id": "570e83bf0b37ab737ca13dd7",
    "notes": "A Destination without a Meta Message",
    "url": "http://www2.dollargeneral.com/Customer-Care-Center/pages/product-recalls.aspx",
    "proximity": 1,
    "metaMessageActive": false,
    "name": "Recalls"
  },
  {
    "_id": "5727baba2095629e622c2913",
    "notes": "A Destination with a Meta Message",
    "url": "http://google.com",
    "metaMessage": "573a372ba78feff835169137",
    "proximity": 2,
    "metaMessageActive": true,
    "name": "Destination Update API"
  }
]
```

#### GET `/api/v2/destinations/:id`

The endpoint for an individual destination with populated properties. It requires the ID of the destination.

Example payload:

```
{
    "_id": "5727baba2095629e622c2913",
    "notes": "An individual destination with a meta message",
    "url": "http://google.com",
    "metaMessage": {
        "_id": "573a372ba78feff835169137",
        "title": "My Title",
        "description": "My Description",
        "faviconUrl": "https://example.com/favicon.png",
        "imageUrl": "https://example.com/image.png"
    },
    "proximity": 2,
    "metaMessageActive": true,
    "name": "Destination woohoo"
}
```

#### POST `/api/v2/destinations`

Create a new `Destination` resource with / without a `Meta Message` resource.

Parameters that can be passed up:

|Parameter|Example|Notes|
|:---:|:---|:---:|
|"name"|"Landing Page"|`String` defaults to "My Destination" - Optional|
|"notes"|"a url for our landing page!"|`String` - Optional.|
|"url"|"https://www.google.com"|`String` - Required.|
|"metaMessage"|<pre>{<br> "title": "Landing on Google",<br> "description": "a custom description of google"<br>}</pre>|`Object` - Optional.  See [CoverCard](https://github.com/bkon-connect/phy-api-docs/wiki/CoverCards)™ API docs for more options|
|"metaMessageActive"|true|`Boolean` - defaults to `false`.  Optional.|
|"tapAction"|<pre>{<br> "actionType": "Call",<br> "to": "555-867-5309"</br>}</pre>|`Object` - Optional.  See [Tap Action API docs](https://github.com/bkon-connect/phy-api-docs/wiki/Tap-Actions) for more options|
|"tapActionActive"|true|`Boolean` - defaults to `false`.  Optional.|
|"proximity"|2|`Int` - defaults to `2`.  Can be `-1`, `0`, `1`, `2`|

`200` Response Payload returns the newly created instance of a `Destination`.  Example:

```
{
    "notes":"a url for our landing page!",
    "url":"https://www.google.com",
    "metaMessage":"5760549780b69d2a67c4443d",
    "_id":"5760549780b69d2a67c4443c",
    "proximity":2,
    "metaMessageActive":true,
    "name":"Landing Page"
}
```

#### PUT or PATCH `/api/v2/destinations/:id`

Update an existing `Destination` by `Destination` ID.

Arguments:

|Parameter|Example|Notes|
|:---:|:---|:---:|
|"name"|"Landing Page"|`String` defaults to "My Destination" - Optional|
|"notes"|"a url for our landing page!"|`String` - Optional.|
|"url"|"https://www.google.com"|`String` - Required.|
|"metaMessage"|<pre>{<br> "title": "Landing on Google",<br> "description": "a custom description of google"<br>}</pre>|`Object` - Optional.  See [CoverCard](https://github.com/bkon-connect/phy-api-docs/wiki/CoverCards)™ API docs for more options|
|"metaMessageActive"|true|`Boolean` - defaults to `false`.  Optional.|
|"tapAction"|<pre>{<br> "actionType": "Call",<br> "to": "867-5309"<br>}</pre>|`Object` - Optional.  See [TapActions API docs](https://github.com/bkon-connect/phy-api-docs/wiki/Tap-Actions) for more options|
|"tapActionActive"|true|`Boolean` - defaults to `false`.  Optional.|
|"proximity"|2|`Int` - defaults to `2`.  Can be `-1`, `0`, `1`, `2`|

Example response:
```
{
    "_id":"5760549780b69d2a67c4443c",
    "notes":"an updated url for our landing page!",
    "url":"https://www.google.com",
    "metaMessage":{
        "_id":"5760549780b69d2a67c4443d",
        "title":"Landing on Google",
        "description":"a custom description of Google",
        "imageUrl":null,
        "faviconUrl":null
    },
    "proximity":1,
    "metaMessageActive":true,
    "name":"Landing Page Updated"
}
```

#### DELETE `/api/v2/destinations/:id`

Delete an existing `Destination` via `Destination` ID

There is no response other than a `204` status code


#### ERRORS

Upon error, the client will receive a `JSON` response in the format of:

```
{
  message: <intl error message>,
  error: <boolean>,
  statusCode: <int>
}
```
