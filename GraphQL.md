# APIs are in the house!
- your thermostat/smartwatch/Alexa
- twitter, linkedin
- wheather

## How?
- to consume APIs you need a client program and the expected shape of the query (you can be a system)
- to produce APIs you need to implement a server that provides queries, mutations and subscriptions

## Why GraphQL? Why?
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

## Cooler than the REST
- avoids over-fetching and under-fetching
- single endpoint, simplifies maintenance and security
- unlimited depth of queries, helps with roundtrips for phone use
- better dev tools

## More info?
- GraphQL playground: https://graphql.org/swapi-graphql/
