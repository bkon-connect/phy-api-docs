### Overview

MicroSites Content is created as a response via the API to `microsites`.

<table>
  <tr>
    <th>parameters</th>
    <th>example</th>
    <th>notes</th>
  </tr>
  <tr>
    <td>contentType</td>
    <td>'Paragraph'</td>
    <td>Can be 'Paragraph', 'Header', 'SubHeader', 'ImageUrl', 'Content'</td>
  </tr>
  <tr>
    <td>body</td>
    <td>'Hello World'</td>
    <td>`String` or `Content` - either the string, or an array of Content objects</td>
  </tr>
  <tr>
    <td>meta</td>
    <td>`{className: 'my-paragraph', title: 'hello title'}`</td>
    <td>`Object` - optional and contains 2 optional properties of className and title</td>
  </tr>
  <tr>
    <td>meta.className</td>
    <td>'my-paragraph'</td>
    <td>`String` - name of a class to put on this piece of content</td>
  </tr>
  <tr>
    <td>meta.title</td>
    <td>'hello title'</td>
    <td>`String` - content of the html title attribute</td>
  </tr>
</table>

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

<table>
  <tr>
    <th>contentType</th>
    <th>class</th>
  </tr>
  <tr>
    <td>Paragraph</td>
    <td>`.phy-microsite__paragraph`</td>
  </tr>
  <tr>
    <td>Header</td>
    <td>`.phy-microsite__header`</td>
  </tr>
  <tr>
    <td>SubHeader</td>
    <td>`.phy-microsite__sub-header`</td>
  </tr>
  <tr>
    <td>ImageUrl</td>
    <td>`.phy-microsite__image`</td>
  </tr>
  <tr>
    <td>Content</td>
    <td>`.phy-microsite__container`</td>
  </tr>
</table>
