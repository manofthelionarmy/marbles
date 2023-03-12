[Introduction to Hypermedia Rest](https://www.mscharhag.com/api-design/hypermedia-rest)
# Summary:
---
# Related Stuff:
---
# Notes:
- According to the author in *JSON at Work*, it looks like there's two camps for people with and against Hypermedia. The author stated they are with it, but there other alternatives to it. 
- What is Hypermedia?
	- the <mark style="background: #FFB86CA6;">actions</mark> the user can take on the data, along with a <mark style="background: #FFB86CA6;">representation</mark> of how to <mark style="background: #FFB86CA6;">trigger</mark> that action
	- Example:
```json
{
    "_links": {
        "edit-form": {
            "href": "http://example.com/users/1?form=edit",
            "type": "text/html",
            "title": "Edit user"
        }
    }
}
```
- Pretty much, the response contains links to other rest endpoints to get more information or do other actions (like hit a webhook, etc).
- There are different formats for Hypermedia (think of it as different styles or approaches to implementation).
- One of the arguments against hypermedia is that you should document your API really well so that you don't have to use hypermedia in the first place.
- It appears that Hypermedia may be used rarely, so this is something good to know, especially if I come across it.
## Hypermedia response formats
*(I ripped this from the link I shared...)*

So far we just added _links_ elements to our JSON representation. However, it can be a good idea to look at some common Hypermedia response formats before building a Hypermedia REST API. Unfortunately there is no single standard format. Instead, we can choose from a lot of different formats.

Here are some examples:

-   [HAL (Hypertext Application Language)](http://stateless.co/hal_specification.html)
-   [JSON LD (JSON for Linking Data)](https://json-ld.org/)
-   [Collection+JSON](https://github.com/collection-json/spec)
-   [Siren](https://github.com/kevinswiber/siren)
-   [JSON Hyper Schema](https://tools.ietf.org/html/draft-zyp-json-schema-03#section-6)**