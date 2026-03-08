## GraphQL Introduction
Query language for API which uses a type system you define your data. 

### Describe your API with a type system (for backend engineers)
A GraphQL service is created by defining types and their fields, and then writing a function for each field to provide the required data.

#### Type 
![Defining Types Example](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-types.png)

#### Function 
![Defining Functions Example](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-functions.png)


Function will provide data for the me and name fields.


### Query exactly what you need 

After a GraphQL service is running, it can receive GraphQL queries. The service first checks a query to ensure it only refers to the types and fields defined for the API and then runs the provided functions to produce a result


## Schemas and Types

The GraphQL type system describes what data can be queried from the API. The collection of those capabilities is referred to as the service’s schema. 
In querying GraphQL,  it’s useful to have an exact description of the data we can request (what fields, what type of objects, do fields have subfields?)

Right now there are 6 kinds of GraphQL type definitions. 

### Object Type 
Represents a list of named fields

![Object Type Example](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-object-type.png)

- Character is an object type, which means it is comprised of fields
- name and appearsIN are fields in object Character. These are the only 2 fields that can be queried from object Character.
- String is a built-in sacalar type (text).
- [Episode]! is a list type (array) of Epsiode objects
- ! makes the field required/ Non-null

#### Arguments

![Argument Example](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-arguments.png)
Every field in a GraphQL type can have zero or more arguments. All arguments must be named unlike Python w/c can take ordered arguments. 
Arguments can be optional or required. When it's optional, we can define a default value. 

In the example, length field has a unit argument which, when not provided, has a default value of METER. 


### Scalar Types
An object type has a name and fields, but these fields should have defined types. 
Scalar types are usually used to declare types of the leaf values of a query. 
- INT: signed 32-bit integer
- STRING: UTF-8 char sequence
- FLOAT: double-precision floating-point value
- BOOLEAN: true/false
- ID: A unique identifier, serialized same as a string

We can also define custom scalar types eg: 

![Custom Scalar Type Definition](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-custom-scalar-type.png)

### Enum Type
Special type of scalar type that restrict allowed field values to set of allowable values. 

![Enum Type Definition](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-enum-type.png)


### Interface Type
GraphQL interfaces represent a list of named fields and their arguments, which can be used to be implemented on Objects and other interfaces. 

For example, you could have a Character Interface type that represents any character in the Star Wars trilogy:

![Character Interface](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-interface-type.png)

Any type that implements Character needs to have these exact fields as well as the same arguments and return types.

For example, here are some types that might implement Character:

![Character Implementation Example](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-interface-implementation.png)

You can see that both of these types have all of the fields from the Character Interface type, but also bring in extra fields.


### Union Type
GraphQL Unions represent an object that could be one of a list of GraphQL Object types, but provides for no guaranteed fields between those types

![Union Type Definitaion Example](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-union-type.png)
Wherever we return a SearchResult type in our schema, we might get a Human, a Droid, or a Starship. Note that members of a Union type need to be concrete Object types

You need to use an *inline fragment* to be able to query any fields that are defined on the member Object types:

![Union Type Querying Sample](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-union-type-querying.png)
- Query on search field that requires a text argument, and returns the SearchResult Union type
- __typename is a GraphQL meta-field. It tells you the actual type of each returned item. Helpful because every return item may be of type Human, Droid, or Starship.
- Inline fragments (... on Type) allows to select which fields to return on each type


### Input Object Type
This is the type of the arguments passed to fields

![Input Object Type Sample](https://github.com/blumea7/BusinessIntelligence/blob/main/assets/graphql-input-object-type.png)
