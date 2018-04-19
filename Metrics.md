For access to the `/api/v2/metrics` endpoints you must be [Authenticated](Authentication.md)

#### GET `/api/v2/metrics/stats`

The main metrics endpoint

Query Params:

|Query Param|Example|Notes|
|:---|:---|:---|
|metric|`scans`|`String` - Required. Valid metrics: `scans`, `taps`|
|from*|`1521561000000`|`Number` - Required. Date in Milliseconds|
|to*|`1524153000000`|`Number` - Required. Date in Milliseconds. to _must_ be after from|
|dimension|`activity`|`String` - Required. Valid dimensions: `activity`, `phyid`, `app`, `destination`, `os`|
|value|`["abc123"]`|`String`or `Array` - Required. Valid values are `all` or an array of IDs for the given dimension|
|interval|`hour`|`String` - Required. Valid intervals: `15min`, `hour`, `day`, `week`, `month`, `quarter`, `year`|
|touchpoint|`abc123`|`String` - Optional, will be deprecated in favor of more robust dimensions. Secondary dimension to pin down further on `destination` dimension|

*NOTE: `stats` is limited by the number of responses based on the `interval`, `from`, and `to`, with the following table:
 
|Interval| Max Range|
|:---:|:---:|
|`15min`|24 hours|
|`hour`|3 days|
|`day`|91 days|
|`week`|1 year|
|`month`|2 years|
|`quarter`|4 years|

Example Request: 
```
https://my.phy.net/api/v2/metrics/stats?metric=scans&from=1521561000000&to=1524153000000&dimension=activity&value=all&interval=day
```

Example response:

```
{
    "account": [
        [
            1521590400000,
            26
        ],
        [
            1521676800000,
            20
        ],
        [
            1521763200000,
            37
        ],
        [
            1521849600000,
            85
        ],
        [
            1521936000000,
            90
        ],
        [
            1522022400000,
            67
        ],
        [
            1522108800000,
            116
        ],
        [
            1522195200000,
            205
        ],
        [
            1522281600000,
            40
        ],
        [
            1522368000000,
            69
        ],
        [
            1522454400000,
            68
        ],
        [
            1522540800000,
            39
        ],
        [
            1522627200000,
            46
        ],
        [
            1522713600000,
            29
        ],
        [
            1522800000000,
            224
        ],
        [
            1522886400000,
            63
        ],
        [
            1522972800000,
            33
        ],
        [
            1523059200000,
            68
        ],
        [
            1523145600000,
            140
        ],
        [
            1523232000000,
            23
        ],
        [
            1523318400000,
            56
        ],
        [
            1523404800000,
            29
        ],
        [
            1523491200000,
            35
        ],
        [
            1523577600000,
            54
        ],
        [
            1523664000000,
            64
        ],
        [
            1523750400000,
            80
        ],
        [
            1523836800000,
            72
        ],
        [
            1523923200000,
            135
        ],
        [
            1524009600000,
            76
        ],
        [
            1524096000000,
            17
        ]
    ]
}
```

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
