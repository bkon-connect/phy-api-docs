# API V2 Beacons

For access to the /api/v2/beacons endpoint you must be [Authenticated](Authentication.md)
<br><br>
### GET `/api/v2/beacons`

Index endpoint for returning all beacons that belong to the user's account.  Example payload:

```
[
    {
        "_id" : "7FBDBb",
        "desc" : "example",
        "firmwareVersion" : "int",
        "urlTags" : {
            "custom" : [
                {
                    "key" : "",
                    "value" : "",
                    "active" : false
                },
                {
                    "key" : "",
                    "value" : "",
                    "active" : false
                }
            ],
            "phyTimeActive" : false,
            "phyIDActive" : false
        },
        "install" : {
            "brand" : "-1",
            "details" : "",
            "locationAddress" : "",
            "locationName" : "",
            "locationType" : "fixed",
            "photo" : {
                "close" : "",
                "far" : "",
                "immediate" : ""
            },
            "source" : "usb"
        },
        "disabled" : false,
        "name" : "Front Door",
        "thirdParty" : false,
        "proximity" : 2,
        "redirectUrl" : "https://bkon.com/next-steps/",
        "folder": ObjectId("example"),
        "destination" : ObjectId("example"),
        "batteryLevel" : 0.1,
        "batteryVoltage" : 2.05,
        "advertisingRate" : 700,
        "advertisingMode": 257,
        "delimiter" : "?",
        "eddyType" : 16,
        "mode" : 257,
        "address": "DAC358A4E6B5",
        "rtkInterval" : 61200,
        "txPower" : -4,
         tlmInterval: 0,
        "uidNamespace" : "C48C6716C550CE582A22",
        "uuid" : "C48C6716-193F-477B-B73A-C550CE582A22"
        "major": 2000,
        "minor": 5823,
        "metaMessage": ObjectId("example"),
        "metaMessageActive": true
    },
    ...
]
```
<br>

**GET Query Params for INDEX**
<br>
The following query parameters can be appended to the `GET` request:

|Query Parameter|Example|Notes|
|:---:|:---:|:---:|
|limit|`/api/v2/beacons?limit=5`|Number of beacons to return in the payload|
|skip|`/api/v2/beacons?skip=5`|Number of beacons to skip over when fetching|
|sort|`/api/v2/beacons?sort=name`|The beacon field to sort the payload by|

An example of paginating a list of beacons by name would be:

Page 1 -> `api/v2/beacons?limit=5&sort=name`

Page 2 -> `api/v2/beacons?limit=5&skip=7&sort=name`
<br><br>
#### GET `/api/v2/beacons/:id`

Show endpoint for returning a fully populated `Beacon`.  Example payload:

```
[
    {
        "_id" : "7FBDBb",
        "desc" : "example",
        "firmwareVersion" : "int",
        "urlTags" : {
            "custom" : [
                {
                    "key" : "",
                    "value" : "",
                    "active" : false
                },
                {
                    "key" : "",
                    "value" : "",
                    "active" : false
                }
            ],
            "phyTimeActive" : false,
            "phyIDActive" : false
        },
        "install" : {
            "brand" : "-1",
            "details" : "",
            "locationAddress" : "",
            "locationName" : "",
            "locationType" : "fixed",
            "photo" : {
                "close" : "",
                "far" : "",
                "immediate" : ""
            },
            "source" : "usb"
        },
        "disabled" : false,
        "name" : "Front Door",
        "thirdParty" : false,
        "proximity" : 2,
        "redirectUrl" : "https://bkon.com/next-steps/",
        "folder": "ObjectId(example)",
        "destination" : {
            "_id": "5727baba2095629e622c2913",
            "notes": "An individual destination with a meta message",
            "url": "http://google.com",
            "metaMessage": {
                "_id": "573a372ba78feff835169137",
                "title": "My Title",
                "description": "My Description"
            },
            "proximity": 2,
            "metaMessageActive": true,
            "name": "Destination woohoo"
        },
        "batteryLevel" : 0.1,
        "batteryVoltage" : 2.05,
        "advertisingRate" : 700,
        "advertisingMode": 257,
        "delimiter" : "?",
        "eddyType" : 16,
        "mode" : 257,
        "address": "DAC358A4E6B5",
        "rtkInterval" : 61200,
        "txPower" : -4,
        "tlmInterval": 0,
        "uidNamespace" : "C48C6716C550CE582A22",
        "uuid" : "C48C6716-193F-477B-B73A-C550CE582A22",
        "major": 2000,
        "minor": 5823,
        "metaMessage": {
            "_id": "573a372ba78feff835169137",
            "title": "My Title",
            "description": "My Description",
            "faviconUrl": "http://example.com/image",
            "imageUrl": "http://example.com/image"
        },
        "metaMessageActive": true
    }
]
```
<br><br>
#### PUT/PATCH `/api/v2/beacons/:id`

Update endpoint for beacons.  Parameters are:

|Parameter|Example|Notes|
|:---:|:---|:---:|
|"redirectUrl"|"https://google.com"|`String` - Required.|
|"desc"|"Description of the beacon"|`String` - Optional.|
|"destination"|"aefoiawe123"|`ObjectId` of `Destination` instance - Optional.|
|"disabled"|true|`Boolean` defaults to false.  Optional.|
|"install"|<pre>{<br>"install":<br>{<br> "brand": "-1",<br> "details": "",<br> "locationAddress": "",<br> "locationName": "",<br> "locationType": "fixed",<br> "photo": {<br>  "close": "",<br>  "far": "",<br>  "immediate": ""<br>  }<br> }<br>}</pre>|All except `photo` are type `String` including the `photo` properties.  All are Optional.|
|"urlTags"|<pre>{<br>"custom": [<br> {<br>  "key": "",<br>  "value: "",<br>  "active": false<br>  }<br> ]<br> "phyTimeActive": false,<br> "phyIDActive": false<br>}</pre>|`custom` is an array of objects which contain:<br>(a) "key" - `String` optional<br>(b) "value" - `String` optional<br>(c) "active" - `Boolean` defaults to false.  Optional<br><br>"phyTimeActive" - `Boolean` defaults to false<br>"phyIDActive" - `Boolean` defaults to false|
|"metaMessageActive"|true|`Boolean` - Optional.|
|"metaMessage"|<pre>{<br>  "title": "example",<br>  "description": "example",<br>  "faviconUrl": "https://url.to.image",<br>  "imageUrl": "https://url.to.image"<br>}</pre>|See [CoverCards API](CoverCards.md) for properties and description|

Upon update, the fully populated, updated document will be returned.  See `GET /api/v2/beacons/:id` example payload for example return.

<br><br>
#### PUT/PATCH `/api/v2/beacons/claim`

Claim a beacon.  Submit a PUT request with an array beacon IDs.  Example:

```
'{"beaconIds": ["abc123", "xyz456"]}'
```
Parameter Options:

|Parameter|Example|Notes|
|:---:|:---|:---:|
|"redirectUrl"|"https://google.com"|`String` - Required.|
|"desc"|"Description of the beacon"|`String` - Optional.|
|"destination"|"aefoiawe123"|`ObjectId` of `Destination` instance - Optional.|
|"disabled"|true|`Boolean` defaults to false.  Optional.|
|"install"|<pre>{<br>"brand": "BKON",<br>"details": "",<br>"locationAddress": "",<br>"locationName": "jhggjhk",<br>"source": "Alk",<br>"photo": {<br> "close": "",<br> "far": "",<br> "immediate": ""<br> } <br>}</pre>|All except `photo` are type `String` including the `photo` properties.  All are Optional.|
|"urlTags"|<pre>{<br>"custom": [<br> {<br>  "key": "",<br>  "value: "",<br>  "active": false<br> }<br>],<br> "phyTimeActive": false,<br> "phyIDActive": false<br>}</pre>|`custom` is an array of objects which contain:<br><br>(a) "key" - `String` optional<br>(b) "value" - `String` optional<br>(c) "active" - Boolean defaults to false.  Optional<br><br>"phyTimeActive" - `Boolean` defaults to false<br>"phyIDActive" - `Boolean` defaults to false|
|"metaMessageActive"|true|Boolean - Optional.|
|"metaMessage"|<pre>{<br> "title": "example",<br> "description": "example",<br> "faviconUrl": "https://url.to.image",<br> "imageUrl": "https://url.to.image"<br>}<br></pre>|See [CoverCards API](CoverCards.md) docs for properties and description|

Example response:

`200` status code.  If the client requires a refresh of the beacons, do a fetch from the `/api/v2/beacons/ endpoint`.

```
{
  "message": "Beacons assigned.",
  "validIds": ["abc123", "xyz456"],
  "invalidIds": []
}
```

`validIds` are Beacon IDs that have been successfully claimed.  `invalidIds` are ones that were not.  An example of an invalidId would be a phyId that does not exist.

Upon claim, a the fully populated, updated document will be returned.  See `GET /api/v2/beacons/:id` example payload for example return.
<br><br>
#### DELETE `/api/v2/beacons/:id/release`

Release a beacon.

Upon deletion a 200 status code will be returned.
<br><br>
