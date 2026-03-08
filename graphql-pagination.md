## Pagination
Traverse lists of objects with a consistent field pagination model


### Plurals
The simplest way to expose a connection between objects is with a field that returns a plural List type.

![Plural List](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-plurals.png)


### Slicing
Client might want to be able to specify how many friends they want to fetch — maybe they only want the first two.

![Slicing Results](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-slicing.png)

But if we just fetched the first two, we might want to paginate through the list as well;

### Pagination

Ways to do pagination:

-  Offset-based: `friends(first:2 offset:2)` to ask for the next two in the list.
-  ID-based:  `friends(first:2 after:$friendId)`, to ask for the next two after the last friend we fetched.
-  Cursor-based: `friends(first:2 after:$friendCursor)`, where we get a cursor from the last item and use that to paginate.


In general, we’ve found that cursor-based pagination is the most powerful of those designed.
Cursors are opaque and their format should not be relied upon, we suggest base64 encoding them.

But that leads us to a problem—how do we get the cursor from the object?
So we might want to introduce a new layer of indirection; our friends field should give us a list of edges, and an edge has both a cursor and the underlying node:
