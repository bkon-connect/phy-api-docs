# API V2 Apps

For access to the /api/v2/apps endpoint you must be [Authenticated](https://github.com/bkon-connect/phy-api-docs/wiki/Authentication)

#### GET `/api/v2/apps`

Index endpoint for all apps in an account. Example response:
```
[
  {
    "_id": "58ffbc01860fc2ff4cb2afd2",
    "updatedAt": "2017-05-12T19:35:38.355Z",
    "createdAt": "2017-04-25T21:13:37.000Z",
    "uuid": "08da2ae6-694f-5848-828a-32418a0ce8e9",
    "createdBy": 562,
    "account": 509,
    "__v": 0,
    "modifiedBy": 562,
    "notes": "",
    "filterType": "ACCOUNT",
    "passPhyIq": false,
    "deactivated": false,
    "name": "testing"
  }
]
```

#### GET `/api/v2/apps/:id`

Show endpoint for retrieving a specific app's details. Example response:
```
{
  "_id": "58ffbc01860fc2ff4cb2afd2",
  "updatedAt": "2017-05-12T19:35:38.355Z",
  "createdAt": "2017-04-25T21:13:37.000Z",
  "uuid": "08da2ae6-694f-5848-828a-32418a0ce8e9",
  "createdBy": 562,
  "account": 509,
  "__v": 0,
  "modifiedBy": 562,
  "notes": "",
  "filterType": "ACCOUNT",
  "passPhyIq": false,
  "deactivated": false,
  "name": "testing"
}
```


#### GET `/api/v2/apps/:id/beacons`

Index endpoint for all beacons in an account that have different settings for a given app. The beacon is fully populated. Example response:
```
[
  {
    "_id": "59160e8123cea55b19b945ee",
    "app": "58ffbc01860fc2ff4cb2afd2",
    "beacon": {
      "_id": "uQxQvx",
      "desc": "",
      "order_id": 88,
      "firmwareVersion": "",
      "__v": 2,
      "account_id": 509,
      "destination": "570e83d90b37ab737ca13de2",
      "batteryLevel": 0.94,
      "batteryVoltage": 2.9749999999999996,
      "touchpointType": "Beacon",
      "redirectUrl": "https://bkon.com/next-steps/",
      "name": "Checkout #1",
      "disabled": false,
      "install": {
        "brand": "-1",
        "details": "",
        "locationAddress": "",
        "locationName": "",
        "source": "usb",
        "photo": {
          "close": "",
          "far": "",
          "immediate": ""
        }
      },
      "urlTags": {
        "phyIDActive": true,
        "phyTimeActive": true,
        "custom": [
          {
            "key": "",
            "value": "",
            "_id": "570e85ba0b37ab737ca13e91",
            "active": false
          },
          {
            "key": "",
            "value": "",
            "_id": "570e85ba0b37ab737ca13e90",
            "active": false
          }
        ]
      },
      "metaMessage": null,
      "metaMessageActive": false,
      "eidScalar": 5,
      "uuid": "C48C6716-193F-477B-B73A-C550CE582A22",
      "delimiter": "?",
      "rtkInterval": 61200,
      "tlmInterval": 0,
      "uidNamespace": "C48C6716C550CE582A22",
      "advertisingMode": 257,
      "eddyType": 16,
      "txPower": -12,
      "advertisingIntervals": [],
      "advertisingRate": 1120,
      "spoofStatus": {
        "count": 0
      },
      "secure": false,
      "thirdParty": false,
      "proximity": 2
    },
    "filterIncludes": true,
    "deactivated": false
  }
]
```

#### GET `/api/v2/apps/:id/beacons/:beaconId`

Show endpoint for the relationship between a beacon and an app. Includes the beacon, fully populated. Response example:
```
{
  "_id": "59160e8123cea55b19b945ee",
  "app": {
    "_id": "58ffbc01860fc2ff4cb2afd2",
    "updatedAt": "2017-05-12T19:35:38.355Z",
    "createdAt": "2017-04-25T21:13:37.000Z",
    "uuid": "08da2ae6-694f-5848-828a-32418a0ce8e9",
    "createdBy": 562,
    "account": 509,
    "__v": 0,
    "modifiedBy": 562,
    "notes": "",
    "filterType": "ACCOUNT",
    "passPhyIq": false,
    "deactivated": false,
    "name": "testing"
  },
  "beacon": {
    "_id": "uQxQvx",
    "desc": "",
    "order_id": 88,
    "assigned": true,
    "firmwareVersion": "",
    "authKey": "C7E3C1731684B7A350AB7D8916ED97B2",
    "__v": 2,
    "account_id": 509,
    "destination": "570e83d90b37ab737ca13de2",
    "batteryLevel": 0.94,
    "batteryVoltage": 2.9749999999999996,
    "touchpointType": "Beacon",
    "redirectUrl": "https://bkon.com/next-steps/",
    "name": "Checkout #1",
    "disabled": false,
    "install": {
      "brand": "-1",
      "details": "",
      "locationAddress": "",
      "locationName": "",
      "source": "usb",
      "photo": {
        "close": "",
        "far": "",
        "immediate": ""
      }
    },
    "urlTags": {
      "phyIDActive": true,
      "phyTimeActive": true,
      "custom": [
        {
          "key": "",
          "value": "",
          "_id": "570e85ba0b37ab737ca13e91",
          "active": false
        },
        {
          "key": "",
          "value": "",
          "_id": "570e85ba0b37ab737ca13e90",
          "active": false
        }
      ]
    },
    "metaMessage": null,
    "metaMessageActive": false,
    "eidScalar": 5,
    "uuid": "C48C6716-193F-477B-B73A-C550CE582A22",
    "delimiter": "?",
    "rtkInterval": 61200,
    "tlmInterval": 0,
    "uidNamespace": "C48C6716C550CE582A22",
    "advertisingMode": 257,
    "eddyType": 16,
    "txPower": -12,
    "advertisingIntervals": [],
    "advertisingRate": 1120,
    "spoofStatus": {
      "count": 0
    },
    "secure": false,
    "thirdParty": false,
    "proximity": 2
  },
  "filterIncludes": true,
  "deactivated": false
}
```


#### PUT `/api/v2/apps/:id/beacons/:beaconId`

Update endpoint for beacons.  Parameters are:
<table>
  <tr>
    <th>Parameter</th>
    <th>Example</th>
    <th>Notes</th>
  </tr>
  <tr>
    <td>"url"</td>
    <td>"https://google.com"</td>
    <td>`String` - Required.</td>
  </tr>
  <tr>
    <td>"notes"</td>
    <td>"Description of the beacon"</td>
    <td>`String` - Optional.</td>
  </tr>
  <tr>
    <td>"destination"</td>
    <td>"aefoiawe123"</td>
    <td>`ObjectId` of `Destination` instance - Optional.</td>
  </tr>
  <tr>
    <td>"deactivated"</td>
    <td>true</td>
    <td>`Boolean` - Optional. If false, the beacon will follow alternate redirection rules as defined here.</td>
  </tr>
  <tr>
    <td>"persistent"</td>
    <td>true</td>
    <td>`Boolean` - Optional. If true, the beacon will always show within the app</td>
  </tr>
  <tr>
    <td>"persistentPosition"</td>
    <td>true</td>
    <td>`String` - Options: 'above', 'below'. Determines whether a persistent touchpoint shows above or below non-persistent touchpoints. </td>
  </tr>
  <tr>
    <td>"filterIncludes"</td>
    <td>true</td>
    <td>`Boolean` - Optional. Only relevant if app's `filterLevel` is `ACCOUNT`. If false, the touchpoint will not appear in that app.</td>
  </tr>
</table>


Upon update, the fully populated, updated document will be returned.  See `GET /api/v2/apps/:id/beacons/:beaconId` example payload for example return.
