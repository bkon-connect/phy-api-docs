The `Tap Action` resource is special in the sense that it is only created/read/updated/destroyed through other resources.  Currently, this is restricted to `Destination` resources.

The workflow to create a `Destination` on all future resources is done by passing up:

(1) `tapActionActive: <boolean>` to flag if we should have it on or off

(2) `tapAction: <object>` an object of attributes to put on the `Tap Action`

When updating a `Destination` with a `TapAction` that does not currently have one, a new `Tap Action` will be created and bound.

A `Tap Action` must have a valid `actionType` to be saved and set. There are currently four types of `Tap Actions`

### Tap To Call
|Parameter|Example|Notes|
|:---:|:---:|:---:|
|"actionType"|"Call"|`String` - Required.|
|"to"|"111-111-1111"|`String` - Recommended.|

Example payload:

```
{
  "name": "Tap Action Demo",
  "metaMessage": {
    "title": "Call Jenny",
    "description": "Tap to call Jenny"
  },
  "metaMessageActive": true,
  "tapAction": {
    "actionType": "Call",
    "to": "8675309"
  },
  "tapActionActive": true
}
```

Example response:

```
{
    "_id": "591da169402f890100f5ce8a",
    "notes": "new destination for testing",
    "url": "http://example.com",
    "metaMessage": {
        "_id": "591da169402f890100f5ce8b",
        "title": "Call Jenny",
        "description": "Tap to call Jenny"
    },
    "metaMessageActive": true,
    "proximity": 2,
    "name": "Tap Action Demo",
    "tapAction": {
        "_id": "5a258541c0c4950100dae225",
        "updatedAt": "2017-12-04T17:26:25.000Z",
        "createdAt": "2017-12-04T17:26:25.000Z",
        "to": "8675309",
        "actionType": "Call"
    },
    "tapActionActive": true
}
```
<br>


### Tap To Email
|Parameter|Example|Notes|
|:---:|:---:|:---:|
|"actionType"|"Email"|`String` - Required.|
|"to"|"to.tim@test.com"|`String` - Recommended|
|"cc"|"copied.carl@test.com"|`String`|
|"bcc"|"blind.copied.carol@test.com"|`String`|
|"subject"|"Sample Subject"|`String` - Cannot have an email address included|
|"body"|"Bountiful Body of Beauty"|`String` Cannot have an email address included|

Example payload:


```
{
  "name": "Tap Action Demo",
  "metaMessage": {
    "title": "Email us",
    "description": "Tap to send an email"
  },
  "metaMessageActive": true,
  "tapAction": {
    "actionType": "Email",
    "to": "to.tim@test.com",
    "cc": "copied.carl@test.com",
    "bcc": "blind.copied.carol@test.com",
    "subject": "Sample Subject",
    "body": "Bountiful Body of Beauty"
  },
  "tapActionActive": true
}
```



### Tap To Text (SMS)
|Parameter|Example|Notes|
|:---:|:---:|:---:|
|"actionType"|"Sms"|`String` - Required.|
|"to"|"111-111-1111"|`String`|
|"message"|"Meaningful Message"|`String`|

Example payload:

```
{
  "name": "Tap Action Demo",
  "metaMessage": {
    "title": "Text us",
    "description": "Tap to send an text message"
  },
  "metaMessageActive": true,
  "tapAction": {
   "actionType": "Sms", "to": "111-111-1111", "message": "Meaningful Message"
  },
  "tapActionActive": true
}
```


### Developer's Webhook
|Parameter|Example|Notes|
|:---:|:---:|:---:|
|"actionType"|"Webhook"|`String` - Required.|
|"method"|"POST"|`String` Options: [`POST`, `GET`] - Required.|
|"payloadUrl"|"http://example.com"|`String` - Required. This is where you can integrate another API. Here's an [integration with the Slack API](https://help.phyplatform.support/hc/en-us/articles/115002894713-TapAction-Recipe-Message-to-Slack).  |
|"contentType"|"application/json"|`String` Options: `['application/json', 'application/x-www-form-urlencoded']`|
|"successMessage"|"Woooooooo"|`String`|
|"loadingMessage"|"Please wait..."|`String`|
|"failureMessage"|"Oops! An error occurred"|`String`|
