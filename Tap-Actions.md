The `Tap Action` resource is special in the sense that it is only created/read/updated/destroyed through other resources.  Currently, this is restricted to `Destination` resources.

The workflow to create a `Destination` on all future resources is done by passing up:

(1) `tapActionActive: <boolean>` to flag if we should have it on or off

(2) `tapAction: <object>` an object of attributes to put on the `Tap Action`

When updating a `Destination` with a `TapAction` that does not currently have one, a new `Tap Action` will be created and bound.

A `Tap Action` must have a valid `actionType` to be saved and set. There are currently four types of `Tap Actions`

### Tap To Call
<table>
  <tr>
    <th>Parameter</th>
    <th>Example</th>
    <th>Notes</th>
  </tr>
  <tr>
    <td>"actionType"</td>
    <td>"Call"</td>
    <td>`String` - Required.</td>
  </tr>
  <tr>
    <td>"to"</td>
    <td>"111-111-1111"</td>
    <td>`String`</td>
  </tr>
</table>

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
<table>
  <tr>
    <th>Parameter</th>
    <th>Example</th>
    <th>Notes</th>
  </tr>
  <tr>
    <td>"actionType"</td>
    <td>"Email"</td>
    <td>`String` - Required.</td>
  </tr>
  <tr>
    <td>"to"</td>
    <td>"to.tim@test.com"</td>
    <td>`String`</td>
  </tr>
  <tr>
    <td>"cc"</td>
    <td>"copied.carl@test.com"</td>
    <td>`String`</td>
  </tr>
  <tr>
    <td>"bcc"</td>
    <td>"blind.copied.carol@test.com"</td>
    <td>`String`</td>
  </tr>
  <tr>
    <td>"subject"</td>
    <td>"Sample Subject"</td>
    <td>`String` Cannot have an email address included</td>
  </tr>
  <tr>
    <td>"body"</td>
    <td>"Bountiful Body of Beauty"</td>
    <td>`String` Cannot have an email address included</td>
  </tr>
</table>

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
<table>
  <tr>
    <th>Parameter</th>
    <th>Example</th>
    <th>Notes</th>
  </tr>
  <tr>
    <td>"actionType"</td>
    <td>"Sms"</td>
    <td>`String` - Required.</td>
  </tr>
  <tr>
    <td>"to"</td>
    <td>"111-111-1111"</td>
    <td>`String`</td>
  </tr>
  <tr>
    <td>"message"</td>
    <td>"Meaningful Message"</td>
    <td>`String`</td>
  </tr>
</table>

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
<table>
  <tr>
    <th>Parameter</th>
    <th>Example</th>
    <th>Notes</th>
  </tr>
  <tr>
    <td>"actionType"</td>
    <td>"Webhook"</td>
    <td>`String` - Required.</td>
  </tr>
  <tr>
    <td>"method"</td>
    <td>"POST"</td>
    <td>`String` Options: [`POST`, `GET`] - Required.</td>
  </tr>
  <tr>
    <td>"payloadUrl"</td>
    <td>"http://example.com"</td>
    <td>`String` - Required. This is where you can integrate another API. Here's an [integration with the Slack API](https://help.phyplatform.support/hc/en-us/articles/115002894713-TapAction-Recipe-Message-to-Slack).  </td>
  </tr>

  <tr>
    <td>"contentType"</td>
    <td>"application/json"</td>
    <td>`String` Options: `['application/json', 'application/x-www-form-urlencoded']`</td>
  </tr>
  <tr>
    <td>"successMessage"</td>
    <td>"Woooooooo"</td>
    <td>`String`</td>
  </tr>
  <tr>
    <td>"loadingMessage"</td>
    <td>"Please wait..."</td>
    <td>`String`</td>
  </tr>
  <tr>
    <td>"failureMessage"</td>
    <td>"Oops! An error occurred"</td>
    <td>`String`</td>
  </tr>
</table>
