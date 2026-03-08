## Queries 
Learn how to fetch data from a GraphQL server

Suumary of this document:

-  A GraphQL query retrieves data by starting at the query root and traversing through fields to Scalar or Enum leaf values.
-  Fields can have arguments to modify outputs
-  Operations use query, mutation, or subscription keywords to specify type
-  Use of unique operation names aid expression and debugging
-   Field aliases allow renaming response keys and using fields with different arguments
-   Variables, marked with $, provide dynamic values for arguments
-   Fragments are reusable field sets for multiple queries
- Executable directives, like built-in @include and @skip, modify query results on the server.

------------------------------------------------
### Fields 
At its simplest, GraphQL is about asking for specific fields on objects. Let’s start by looking at the hero field that’s defined on the Query type in the schema:

![Sample Field Query](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-sample-field-query.png)

When creating a GraphQL document, we always start with a root operation type (in the example, type Query (default root type)). The root type serves as the entry point of the API. 

Fields can also return Object types, as follows: 

![Sample Object Query](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-sample-object-query.png)

### Arguments

GraphQL also alows passing arguments on fields.

![Sample Argument Definition and Usage](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-arguments.png)

In REST API, arguments can be passed on query strings. In GraphQL, every field can have arguments as long as defined. 

### Operation type and name 
In the examples above we have been using a shorthand syntax where we omit the query keyword before the operation’s selection set.

Long syntax includes *query keyword* and the *unique operation name*. Operation names are useful in production because it makes readability, and traceability easier. 

![Sample Operation Name Usage](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-operation-names.png)

The operation type can be `query`, `mutatoin` or `subscription`, depending on the operation you intend to do. 

### Aliases
Aliases lets you rename the result of a field to anything you want. 

![Sample Use of Aliases](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-aliases.png)

The `hero` field is queried twice, if not renamed using aliases, the `hero` fields would have conlicted. 

### Variables

So far, our arguments are written inside the query string. But in most apps, arguments to fields need to be dynamic. 
Varialbes are a way to store dynamic values.

When working with variables, we need to do these 3 things: 
1) Replace the static value in the query with `$variableName`
2) Declare `$variableName` as one of the variables accepted by the query
3) Pass `variableName: value` in the separate, transport-specific (usually JSON) variables dictionary

![Sample Variable Usage](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-variables.png)


Variable definitions are the part the look like this: `$episode: Episode` -- variable name followed by the expected type of input value. 

Variable types are either Scalar, ENUM, or object. 

Variables can have a default value as follows: 

### Fragments

Imagine we have a complex app page that shows two heroes next to each other, along with their friends. This can make the query complicated because we need to repeat the fields for each hero being compared.
Fragments are best used in this situation. 

*Fragments are reusable units* in GraphQL. Fragments let you construct sets of fields, and then include them in queries where needed. 

![Sample Fragments Use](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-fragments.png)

Variables defined in the operation are accessible to the fragments

![Sample Variable Usage in Fragment](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-variables-in-fragments.png)


### Inline Fragments

If you are querying a field that returns an *Interface or a Union type*, you will need to use *inline fragments* to access data

![Sample Inline Fragments Use](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-inline-fragments.png)

 `hero` field returns the type Character, w/c can be Human or Droid, depending on the value of `$ep`

 To ask for a field on the concrete type, you need to use an *inline fragment with a type condition*. 
 Because the first fragment is labeled as `... on Droid`, the `primaryFunction` field will only be executed if the Character returned from hero is of the Droid type. 
 Similarly for the height field for the Human type.


### Meta Fields 

As we have seen with Union types, there are some situations where you don’t know what type you’ll get back from the GraphQL service

GraphQL allows you to request __typename, a meta field, at any point in a query to get the name of the Object type at that point:

![Sample Use of Meta Field Type Name](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-typename.png)

All field names beginning with two underscores (__) are reserved by GraphQL (e.g., __type, __schema)

### Directives
Extension of making the query dynamic by including/excluding fields depending on the value of passed variables

![Sample Directives use](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-directives.png)

If `withFriends` value is false, then the query response will not include friends data

Two Directives in GraphQL
-  @include(if: Boolean)\
-  @skip(if: Boolean)
