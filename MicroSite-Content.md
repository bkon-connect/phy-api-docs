### Overview

MicroSites Content is created as a response via the API to `microsites`.

|Parameters|Example|Notes|
|:---:|:---|:---:|
|contentType|'Paragraph'|Can be 'Paragraph', 'Header', 'SubHeader', 'ImageUrl', 'Content'|
|body|'Hello World'|`String` or `Content` - either the string, or an array of Content objects|
|meta|<pre>{<br>className: 'my-paragraph',<br>title: 'hello title'<br>}</pre>|`Object` - optional and contains 2 optional properties of className and title|
|meta.className|'my-paragraph'|`String` - name of a class to put on this piece of content|
|meta.title|'hello title'|`String` - content of the html title attribute|


The format of an individual `content` piece is as follows:

```
{ contentType: 'Header', body: 'Hello World!' }
```

These `content` pieces are bound to either a `microsite` content property OR a `content` piece with `contentType: 'Content'`.  An example of a populated `content` body:

```
{
  "content": [{
      "contentType": "Header",
      "body": "1st Header",
      "meta": {
        "className": "header",
        "title": "header"
      }
    },
    {
      "contentType": "Content",
      "body": [{
        "contentType": "Paragraph",
        "body": "test paragraph"
      }, {
        "contentType": "Content",
        "body": [{
          "contentType": "ImageUrl",
          "body": "https://www.dropbox.com/s/zjkag9ro8ocl8v8/meta-name-change.png",
          "meta": {
            "className": "logo-image",
            "title": "name-change"
          }
        }]
      }]
    }
  ]
}
```

The unique `contentType: 'Content'` allows for future dynamic templating and content structures (layouts, etc).

The current possible options for `contentType` are:

`'Paragraph', 'Header', 'SubHeader', 'ImageUrl', 'Content'`

All except `Content` should supply a `String` type as the `body` property.

---

### Styles and Structure

When each `contentType` above is rendered to the page, each of the types receive its own class:

|contentType|class|
|:---:|:---:|
|Paragraph|`.phy-microsite__paragraph`|
|Header|`.phy-microsite__header`|
|SubHeader|`.phy-microsite__sub-header`|
|ImageUrl|`.phy-microsite__image`|
|Content|`.phy-microsite__container`|
