**NOTE: MetaMessage is now CoverCard™.**

The `MetaMessage` resource is special in the sense that it is only created/read/updated/destroyed through a `Destination` resource.

The workflow to create a `Meta Message` on all future resources is done by passing up:

`metaMessage: <object>` an object of attributes to put on the MetaMessage

When updating an `Destination` with a MetaMessage that does not currently have one, a new MetaMessage will be created and bound.

A MetaMessage can be passed the following arguments:

|Parameter|Example|Notes|
|---|---|---|
|"title"|"The title displayed on the Meta Message page"|`String` - Required.|
|"description"|"The description that displays on the meta message page"|`String` - Optional.|
|"imageUrl"|"https://url.to.another.image"|`String` - Optional.|
