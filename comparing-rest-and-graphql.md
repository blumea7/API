## REST API VS GRAPHQL API


|  Item                              |  REST                                              | GRAPHQL                                            |
|----------------------------------- |----------------------------------------------------|--------------------------------------------------- |
|  Query Structure                   |  Uses multiple endpoints for different resources   |  Uses single endpoint for all queries              |
|                                    |  Selection of needed fields done after API Call    |  Fields are selected upon API call                 |
|                                    |                                                    |  Avoids over-fetching and under-fetching           |
|  Data Fetching                     |  May need to make multiple requests to diff endpoints to get all needed data        |  Can fetch all needed data in a single request   |
|  Request Method                    |  HTTP Requests: GET, POST, PUT, DELETE, PATCH      |  Typically uses POST, event for data retrieval     |
|  Responses                         |  Stated in the request (e.g. JSON, XML)            |  Stated in the request                             |
|  Error-Handling                    |  HTTP Error Codes                                  |  Returned in a specific part of the response       |
|  PowerQuery Get Request Requirement|  API Endpoint Base URL and/or Relative Path        |  Query defined as a srting in the request body     |
|                                    |  Headers = creadentials, content-type              |  Familiarity w/ GraphQL syntax and structure       |
|                                    |  Page Size & Number                                |                                                    |
