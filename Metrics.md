For access to the `/api/v2/metrics` endpoints you must be [Authenticated](https://github.com/bkon-connect/phy-api-docs/wiki/Authentication)

#### GET `/api/v2/metrics/metric/:metric/:timerange`

The metrics endpoint that returns metric data for a given metric and timerange.

Parameters:

|Parameter|Example|Notes|
|:---:|:---:|:---:|
|"metric"|"total-scans"|`String` - Required. Valid metrics: `total-scans`, `total-opens`, `scan-open-ratio`, `avg-daily-scans`|
|"timerange"|"today"|`String` - Required. Valid timeranges: `today`, `yesterday`, `last-24-hours`, `this-week`, `last-week`, `last-7-days`, `this-month`, `last-month`, `last-30-days`, `this-quarter`, `last-quarter`, `this-year`, `last-year`|

Example payload:

```
123
```

#### GET `/api/v2/metrics/leaderboard/:metric/:dimension?limit=:limit`

The metrics endpoint that returns leaderboard data for a given metric and dimension, optionally limited.

Parameters:

|Parameter|Example|Notes|
|:---:|:---|:---:|
|"metric"|"total-scans"|`String` - Required. Valid metrics: `total-scans`, `total-opens`|
|"dimension"|"url"|`String` - Required. Valid dimensions: `url`, `beacon`, `app`|
|"limit"|5|`Number` - Optional. Default: 5|

Example payload:

```
{
  "this-week": [
    [
      "abc123",
      123,
      {
        "_id": "abc123",
        "name": "Example Beacon"
      }
    ], [
      "def234",
      77,
      {
        "_id": "def234",
        "name": "Another Beacon"
      }
    ]
  ],
  "this-month": [
    [
      "abc123",
      345,
      {
        "_id": "abc123",
        "name": "Example Beacon"
      }
    ], [
      "def234",
      88,
      {
        "_id": "def234",
        "name": "Another Beacon"
      }
    ]
  ],
  "this-quarter": [
    [
      "abc123",
      567,
      {
        "_id": "abc123",
        "name": "Example Beacon"
      }
    ], [
      "def234",
      99,
      {
        "_id": "def234",
        "name": "Another Beacon"
      }
    ]
  ],
  "this-year": [
    [
      "abc123",
      891,
      {
        "_id": "abc123",
        "name": "Example Beacon"
      }
    ], [
      "def234",
      111,
      {
        "_id": "def234",
        "name": "Another Beacon"
      }
    ]
  ]
}
```

#### GET `/api/v2/metrics/timeline/:metric/:timerange`

The metrics endpoint that returns timeline data for a given metric and timerange.

Parameters:

|Parameter|Example|Notes|
|:---:|:---|:---:|
|"metric"|"total-scans"|`String` - Required. Valid metrics: `total-scans`, `total-opens`|
|"timerange"|"today"|`String` - Required. Valid timeranges: `today`, `yesterday`, `last-24-hours`, `this-week`, `last-week`, `last-7-days`, `this-month`, `last-month`, `last-30-days`, `this-quarter`, `last-quarter`, `this-year`, `last-year`|

Example payload:

```
[
  [
    "2016-07-01T00:00:00.000Z",
    134
  ],
  [
    "2016-07-02T00:00:00.000Z",
    87
  ],
  [
    "2016-07-03T00:00:00.000Z",
    93
  ],
  [
    "2016-07-04T00:00:00.000Z",
    112
  ],
  [
    "2016-07-05T00:00:00.000Z",
    152
  ],
  [
    "2016-07-06T00:00:00.000Z",
    57
  ],
  [
    "2016-07-07T00:00:00.000Z",
    182
  ]
]
```
