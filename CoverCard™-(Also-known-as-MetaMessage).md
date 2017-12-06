**NOTE: MetaMessage is now CoverCard™.**

The `Meta Message` resource is special in the sense that it is only created/read/updated/destroyed through other resources.  Currently, this is restricted to `Event` and `Destination` resources.

The workflow to create a `Meta Message` on all future resources is done by passing up:

(1) `metaMessageActive: <boolean>` to flag if it should be on or off

(2) `metaMessage: <object>` an object of attributes to put on the `Meta Message`

When updating an `Event`, `Destination`, etc. with a `Meta Message` that does not currently have one, a new `Meta Message` will be created and bound.

A `Meta Message` can be passed the following arguments:

<table>
  <tr>
    <th>Parameter</th>
    <th>Example</th>
    <th>Notes</th>
  </tr>
  <tr>
    <td>"title"</td>
    <td>"The title displayed on the Meta Message page"</td>
    <td>String - Required.</td>
  </tr>
  <tr>
    <td>"description"</td>
    <td>"The description that displays on the meta message page"</td>
    <td>String - Required.</td>
  </tr>
  <tr>
    <td>"faviconUrl"</td>
    <td>"https://url.to.some.favicon"</td>
    <td>String - Optional.</td>
  </tr>
  <tr>
    <td>"imageUrl"</td>
    <td>"https://url.to.another.image"</td>
    <td>String - Optional.</td>
  </tr>
</table>
