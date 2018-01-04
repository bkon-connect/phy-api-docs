For access to the `/api/v2/destinations` endpoint you must be [Authenticated](Authentication.md).

#### GET `/api/v2/destinations/`

The index endpoint that returns all destinations for a given user.  Example payload:

```
[
  {
    "_id": "5727baba2095629e622c2913",
    "notes": "A Destination with a Meta Message",
    "metaMessage": "573a372ba78feff835169137",
    "tapAction": "573a372ba78feff835163291",
    "proximity": 2,
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
    "metaMessage": {
        "_id": "573a372ba78feff835169137",
        "title": "My Title",
        "description": "My Description",
        "imageUrl": "https://example.com/image.png"
    },
    "tapAction": {
        "_id": "573a372ba78feff835163291",
        "touchpointType": "Redirect",
        "to": "https://www.phy.net",
    }
    "name": "Destination woohoo"
}
```

#### POST `/api/v2/destinations`

Create a new `Destination` resource with a `Meta Message` and `Tap Action` resource.

Parameters that can be passed up:

|Parameter|Example|Notes|
|:---:|:---|:---:|
|"name"|"Landing Page"|`String` defaults to "My Destination" - Optional|
|"notes"|"a url for our landing page!"|`String` - Optional.|
|"metaMessage"|<pre>{<br> "title": "Landing on Google",<br> "description": "a custom description of google"<br>}</pre>|`Object` - Optional.  See [CoverCards API](CoverCards.md) docs for more options|
|"tapAction"|<pre>{<br> "actionType": "Call",<br> "to": "555-867-5309"</br>}</pre>|`Object` - Optional.  See [Tap Actions API docs](Tap-Actions.md) for more options|

`200` Response Payload returns the newly created instance of a `Destination`.  Example:

```
{
    "notes":"a url for our landing page!",
    "metaMessage":"5760549780b69d2a67c4443d",
    "tapAction": "5727baba2095629e622c2913",
    "_id":"5760549780b69d2a67c4443c",
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
|"metaMessage"|<pre>{<br> "title": "Landing on Google",<br> "description": "a custom description of google"<br>}</pre>|`Object` - Optional.  See [CoverCards API](CoverCards.md) docs for more options|
|"tapAction"|<pre>{<br> "actionType": "Call",<br> "to": "867-5309"<br>}</pre>|`Object` - Optional.  See [TapActions API docs](Tap-Actions.md) for more options|

Example response:
```
{
    "_id":"5760549780b69d2a67c4443c",
    "notes":"an updated url for our landing page!",
    "metaMessage":{
        "_id":"5760549780b69d2a67c4443d",
        "title":"Landing on Google",
        "description":"a custom description of Google",
        "imageUrl":null
    },
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
