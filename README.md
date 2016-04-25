# GraphQL Scouting Report


## Part 1 - An Overview

### The value from a client side perspective

* The process of getting new end points and data being dependent on others schedules
* Cache consistency for data with overlapping structures 
* Maintenance as an api evolves
* Query parameters, paging, and validation
* Living Documentation

### Related Predecessors
* REST such as (Json Api)
    http://jsonapi.org/examples/#pagination
    
* Odata with breeze or jaydata  
    http://www.odata.org/documentation/odata-version-2-0/uri-conventions    
    http://services.odata.org/ODataAPIExplorer/ODataAPIExplorer.html
    http://breeze.github.io/doc-js/query-examples.html     
    
* Breeze schemas entity framework and hand entering metadata 
    http://breeze.github.io/doc-node-mongodb 
    http://breeze.github.io/doc-js/metadata.html

* Falcor
	http://netflix.github.io/falcor/documentation/datasources.html


### Potential Problems
* Security? (will come up but probably not a real issue)
* Complexity (queries still need to be hand written and can be complex)
* Strong typing without strong tooling is worse than no typing at all 
* Creating schemas will be a chore for both strong and weak type systems

  
  
## Part 2 -  The Syntax
  
The syntax is a query language using the best part of js, json

That is it looks like json, until it doesn't, pretty elegant
    
### Example Queries with Swapi	and GraphQLHub
   http://graphql-swapi.parseapp.com/
   https://www.graphqlhub.com/

   https://github.com/graphql/swapi-graphql/tree/master/doc/example_queries
  
### Terminology
  
A visual/aural dictionary of terms on mouseover of a good example query. 

Go through each term in the spec

Schema shorthand and actual syntax


## Part 3 - Testing
types of testing, schema, unit, query, edge cases, validation, end to end, 
* http://graphql.org/blog/mocking-with-graphql/
* https://github.com/rmosolgo/graphql-ruby/blob/master/guides/testing.md
* https://github.com/graphql/graphql-js/tree/master/src/language/__tests__


## Part 4 - Projects
* Apollo http://docs.apollostack.com/
* Graitti https://github.com/RisingStack/graffiti
* Absynthe http://absinthe-graphql.org/guides/writing-schemas/
* GraphQL-Ruby https://github.com/rmosolgo/graphql-ruby

## Part 5 - Articles
   the spec http://facebook.github.io/graphql/
   relay https://facebook.github.io/relay/docs/graphql-relay-specification.html#content

## Part 6 - Tools
* https://github.com/graphql/graphiql
* AST Explorer https://github.com/fkling/astexplorer

## Part 7 - An Example

### A Map for a Board Game
  
### Schema 

    Game:
        name: string
        positions: [Position]
        map: Map
        turns: [Turn]
        current_turn: integer
        status: enum
        next_tick: datetime

    Position:
        name: string
        code: string
        color: integer
        race: race_id
        faction: faction_id
        first_turn: integer
        last_turn: integer
        is_secret: boolean
        game_id: integer

    Map: 
        name: string
        code: string
        game_id: integer
        rows: integer
        cols: integer
        bg: string
        regions: [Region]

    Turn:
        name: string
        game_id: integer
        number: integer
        introduction: text
        results: text
        MapState
        PositionStates
        RegionStates

    Region:
        name: string
        code: string
        row: integer
        col: integer	
        terrrain_type_id: integer
        position_id: integer
        map_id: integer
        money: integer
        materials: integer
        research: integer
        is_secret: boolean
        borders: [RegionsBorder]	

    TerrainType:
        id: integer
        name: string
        code: string
        description: text	

    RegionsBorder:
        name: string
        code: string
        border_type_id: integer
        is_secret: boolean

    BorderType:
        source: region_id
        sink: region_id
        is_directional: boolean

    Race
        id: integer
        name: string
        code: string
        description: text

    Faction
        id: integer
        name: string
        code: string
        description: text