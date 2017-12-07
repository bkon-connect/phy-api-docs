**NOTE: MetaMessage is now CoverCard™.**

The `metamessage` resource is special in the sense that it is only created/read/updated/destroyed through other resources.  Currently, this is restricted to `Event` and `Destination` resources.

The workflow to create a `Meta Message` on all future resources is done by passing up:

(1) `metaMessageActive: <boolean>` to flag if it should be on or off

(2) `metaMessage: <object>` an object of attributes to put on the MetaMessage

When updating an `Event`, `Destination`, etc. with a MetaMessage that does not currently have one, a new MetaMessage will be created and bound.

A MetaMessage can be passed the following arguments:

|Parameter|Example|Notes|
|---|---|---|
|"title"|"The title displayed on the Meta Message page"|`String` - Required.|
|"description"|"The description that displays on the meta message page"|`String` - Required.|
|"faviconUrl"|"https://url.to.some.favicon"|`String` - Optional.|
|"imageUrl"|"https://url.to.another.image"|`String` - Optional.|
