---
tags: postgres, json, database, sql
---

# [[2022-06-23 - Querying Json Fields in Postgres]]

We have a number of things in our postgres database where we store them as json blobs, but sometimes we need to find out what's inside of the json blobs for debugging.

There are two operators that are important to know.

`->` is important because it's the base query operator for json columns. You can use it to get back subobjects from the json.

```
select data->'languages' from configuration where id in (195107, 195101);
```

The above will return a json object of whatever is stored in the languages.

But what if you need a text representation of what is stored? That's when `->>` comes in handy. It's the exact same operator as `->` but instead of returning the json object, it returns it as a string.