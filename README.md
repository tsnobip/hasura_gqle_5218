# Repro setup for  hasura/graphql-engine#5218

Clone this repo, `yarn` or `npm install` to install the dependencies.

`yarn start` or `npm run start` to launch Hasura graphql-engine.

`yarn console` or `npm run console` to launch the console.

In the console make sure you use the Relay API and that you're not logged 
as admin (don't send `x-hasura-admin-secret` header).

Paste this query into GraphiQL:
```graphql
query MyQuery {
  project_connection {
    edges {
      node {
        documents_connection {
          edges {
            node {
              name
            }
          }
        }
      }
    }
  }
}
```

Running this query gives the following error:
```json
{
  "errors": [
    {
      "extensions": {
        "path": "$.selectionSet.project_connection",
        "code": "unexpected"
      },
      "message": "could not lookup \"documents_connection\" in 'project'"
    }
  ]
}
````

But `documents_connection` is listed as a field of `project`.