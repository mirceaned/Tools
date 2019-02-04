# APIs are everywhere
- your thermostat/smartwatch
- twitter, linkedin
- wheather

## How do we make use of all this?
- to consume APIs you need a client program and the expected shape of the query
- to produce APIs you need to implement a server that provides data queries, mutations and subscriptions

## What is GraphQL?
- a specification for APIs (Application Prograaming Interfaces)
- modern replacement for RESTful API
- developed by Facebook to help internal and external teams to query data organized in graphs (posts, friends)

## GraphQL Example

- schema
people(id: ID): Person

Person {
  name: String,
  height: Int,
  mass: Float
}

- query
{
  allPeople {
    people {
      name
      height
      mass
    }
  }
}

- response
{
  "data": {
    "allPeople": {
      "people": [
        {
          "name": "Luke Skywalker",
          "height": 172,
          "mass": 77
        },
        {
          "name": "C-3PO",
          "height": 167,
          "mass": 75
        }]
      }
   }
}   

## Benefits vs REST
- avoids over-fetching and under-fetching
- single endpoint, simplifies maintenance and security
- unlimited depth of queries
- better tools

## More info?
- GrpahQL playground: https://graphql.org/swapi-graphql/
