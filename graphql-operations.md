## GraphQL Operations

|  Feature          | Query                      | Mutation                      | Subscription               |
|-------------------|----------------------------|-------------------------------|----------------------------|
| Purpose           | Fetch data                 | Create, update, Delete data   | Retrieve real-time data    |
| Operation Type    | Read-only                  | Write (with side effects)     | Real-time push from server |
| Execution Style   | One-time request-response  | One-time request-response     | Continuous connection      |
| Transport Protocol| HTTP request               | HTTP request                  | WebSockets (typically)     |
| Schema Keyword    | type Query                 | type Mutation                 | type Subscription          |
