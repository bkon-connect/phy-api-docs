For access to the `/api/v2/events` endpoint you must be [Authenticated](Authentication.md)

#### GET `/api/v2/events`

The index endpoint that returns `current` and `future` events.  Example payload:

```
{
  "current": [
    {
      "_id": "570e88900b37ab737ca13f4d",
      "name": "Black Friday",
      "start": "2016-11-29T03:00:00.000Z",
      "stop": "2016-11-29T10:00:00.000Z",
      'notes": "Black Friday second floor",
      "timezone": "UTC",
      "destinations": ["580fb6a05e197e010019eeb1"],
      "disabled": false,
      "beacons": [
      "7FBDBb"
      ]
    }
  ],
  "future": [
    {
      "_id": "570e87cc0b37ab737ca13efe",
      "name": "Christmas Specials",
      "start": "2016-12-01T10:00:00.000Z",
      "stop": "2016-12-25T18:00:00.000Z",
      "notes": "Christmas event, second floor",
      "timezone": "UTC",
      "destinations": ["580fc3e75e197e010019ef5b"],
      "disabled": false,
      "beacons": [
      "7FBDBb"
      ]
    }
  ]
}
```

#### GET `/api/v2/events/:id`

Show endpoint for an individual event based on event ID.

Example payload:

```
{
  "_id": "570e87cc0b37ab737ca13efe",
  "name": "Christmas Specials",
  "start": "2016-12-01T10:00:00.000Z",
  "stop": "2016-12-25T18:00:00.000Z",
  "beacons": <array of populated beacon objects>,
  "timezone": "UTC",
  "destinations": [{
      "_id": "580fb6a05e197e010019eeb1",
      "updatedAt": "2016-10-27T16:25:34.373Z",
      "createdAt": "2016-10-25T19:46:40.992Z",
      "createdBy": 749,
      "account": 001,
      "notes": "example",
      "metaMessage": "580fb6a05e197e010019eeb2",
      "name": "micro-event"
  }]
}
```

#### POST `/api/v2/events`

Create a new `Event` resource with / without a `Meta Message`

Arguments:

|Parameter|Example|Notes|
|:---:|:---|:---:|
|"name"|"Name of event"|`String` - Optional but Recomended|
|"start"|\["2016-05-15", "09:00"\]|`Array` of `String` items - takes a format of \['yyyy-mm-dd', 'hh:mm'\].  Required.|
|"stop"|\["2016-05-16", "09:00"\]|`Array` of `String` items - takes a format of \['yyyy-mm-dd', 'hh:mm'\].  Required.|
|"timezone"|"America/Los_Angeles"|`String` - Defaults to UTC. Required.  For options see the [list of TZ database times zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) and use the `TZ` column|
|"beacons"|\["123test", "456test"\]|`Array` of `String` items - requires an array of Beacon IDs.  Required.|
|"destinations"|["43951ajdsflka3241"]|`Array` of `String` items (technically a Mongo ObjectId). Id of a destination to bind to this event.  Optional.|

Example Payload without `Meta Message`:
```
{
  "_id":"57643d9274c2962083dd3263",
  "name":"My awesome api event without MM",
  "start":"2016-09-01T12:00:00.000Z",
  "stop":"2016-09-02T12:00:00.000Z",
  "proximity":2,
  "timezone":"America/Los_Angeles",
  "destinations": ["5727baba2095629e622c2913"],
  "beacons":["4c92QZ"]
}
```

#### PUT/PATCH `/api/v2/events/:id`

The update endpoint for individual `Event` resources.  Requires an ID.

Additionally, in order to update an event, ALL update requests must be sent with:

* a list of beacon IDs in array form
* a start and stop time in an array date pair form
* a timezone region (to retain accuracy)

(see below for format)

Arguments

|Parameter|Example|Notes|
|:---:|:---|:---:|
|"name"|"Name of event"|`String` - Optional but Highly Recommended.|
|"start"|\["2016-05-15", "09:00"\]|`Array` of `String` items - takes a format of \['yyyy-mm-dd', 'hh:mm'\]. Required.|
|"stop"|\["2016-05-16", "09:00"\]|`Array` of `String` items - takes a format of \['yyyy-mm-dd', 'hh:mm'\].  Required.|
|"timezone"|"America/Los_Angeles"|`String` - Defaults to UTC. Required.  For options use the [list of TZ database times zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) and use the `TZ` column|
|"beacons"|\["123test", "456test"\]|`Array` of `String` items - takes an array of PhyIDs.  Required.|
|"destinations"|["43951ajdsflka3241"]|`Array` of `String` items (technically a Mongo ObjectId).  ID of a destination to bind to this event. Optional.|

Example payload of updating an `Event` without a `MetaMessage`:
```
{
  "_id":"576450837fcce5d8838b30c2",
  "name":"My awesome api event without MM updated without MM",
  "start":"2016-09-01T19:00:00.000Z",
  "stop":"2016-09-02T19:00:00.000Z",
  "destinations": ["5727baba2095629e622c2913"]
  "beacons":["3sjpaF"],
  "timezone":"America/Los_Angeles"
}
```

#### DELETE `/api/v2/events/:id`

The deletion endpoint for `Event` resources.

There is no response other than a `204` status code.


#### ERRORS

Upon error, the client will receive a `JSON` response in the format of:

```
{
  error: <boolean>,
  message: <intl error message>,
  statusCode: <int>
}
```
