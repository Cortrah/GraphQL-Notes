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
    * http://www.odata.org/documentation/odata-version-2-0/uri-conventions    
    * http://services.odata.org/ODataAPIExplorer/ODataAPIExplorer.html
    * http://breeze.github.io/doc-js/query-examples.html     
    
* Breeze schemas entity framework and hand entering metadata
    * http://breeze.github.io/doc-node-mongodb 
    * http://breeze.github.io/doc-js/metadata.html

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
   * http://graphql-swapi.parseapp.com/
   * https://www.graphqlhub.com/

   * https://github.com/graphql/swapi-graphql/tree/master/doc/example_queries
  
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
* the spec http://facebook.github.io/graphql/
* relay https://facebook.github.io/relay/docs/graphql-relay-specification.html#content

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
        species: species_id
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

    Species
        id: integer
        name: string
        code: string
        description: text

    Faction
        id: integer
        name: string
        code: string
        description: text
        
Static Data
        
        {
          "1": {
            "id": "1",
            "name": "Space Opera",
            "positions": [
              {
                "id": "1",
                "name": "Hyperion Flow",
                "code": "hyp",
                "userId":"2",
                "color": "11223344",
                "firstTurn":1,
                "lastTurn":1,
                "isSecret": false,
                "regions":["1","2"],
                "score":0,
                "tradeValue":5,
                "tradePartners":[],
                "allies":[],
                "money":100,
                "materials":100,
                "research":100,
                "moneyIncome":10,
                "materialIncome":10,
                "researchIncome":10,
                "units":[],
                "items":[]
              },
              {
                "id": "2",
                "name": "AstroDog Pack",
                "code": "hyp",
                "userId":"3",
                "color": "44332211",
                "firstTurn":1,
                "lastTurn":1,
                "isSecret": false,
                "regions":["3","4"],
                "score":0,
                "tradeValue":5,
                "tradePartners":[],
                "allies":[],
                "money":100,
                "materials":100,
                "research":100,
                "moneyIncome":10,
                "materialIncome":10,
                "researchIncome":10,
                "units":[]
              }
            ],
            "maps": [
              {
                "id": "1",
                "name": "Galaxy Map",
                "code": "gm",
                "rows": 2,
                "cols": 2,
                "bg": "galaxy.png",
                "regions": [
                  {
                    "id": "1",
                    "name": "Syrius",
                    "code": "sys",
                    "row": 1,
                    "col": 1,
                    "environmentTypeId": 1,
                    "borders":["1","2"],
                    "isSecret": false
                  },
                  {
                    "id": "2",
                    "name": "Speakeasy",
                    "code": "spk",
                    "row": 1,
                    "col": 2,
                    "environmentTypeId": 1,
                    "borders":["1","3"],
                    "isSecret": false
                  },
                  {
                    "id": "3",
                    "name": "Beelzebub",
                    "code": "bub",
                    "row": 2,
                    "col": 1,
                    "environmentTypeId": 1,
                    "borders":["2","4"],
                    "isSecret": false
                  },
                  {
                    "id": "4",
                    "name": "Frankenberry",
                    "code": "fby",
                    "row": 2,
                    "col": 2,
                    "environmentTypeId": 1,
                    "borders":["3","4"],
                    "isSecret": false
                  }
                ],
                "regionsBorders":[
                  {
                    "id":"1",
                    "name":"Syrius-Speakeasy",
                    "code":"1-2",
                    "sourceRegionId": "1",
                    "sinkRegionId": "2",
                    "borderTypeId": "1",
                    "isSecret": false
                  },{
                    "id":"2",
                    "name":"Syrius-Beelzebub",
                    "code":"1-3",
                    "sourceRegionId": "1",
                    "sinkRegionId": "3",
                    "borderTypeId": "1",
                    "isSecret": false
                  },          {
                    "id":"3",
                    "name":"SpeakEasy-Frankenberry",
                    "code":"2-4",
                    "sourceRegionId": "2",
                    "sinkRegionId": "4",
                    "borderTypeId": "1",
                    "isSecret": false
                  },{
                    "id":"4",
                    "name":"Beelzebub-Frankenberry",
                    "code":"3-4",
                    "sourceRegionId": "3",
                    "sinkRegionId": "4",
                    "borderTypeId": "1",
                    "isSecret": false
                  }
                ],
                "borderTypes":[{
                    "id": "1",
                    "name": "adjacent",
                    "code": "adj",
                    "description": "Allows unrestricted movement at no cost",
                    "isDirectional": "false"
                  }
                ],
                "environmentTypes":[
                  {
                    "id":"1",
                    "name":"clear",
                    "code":"c",
                    "description":"Basic flat terrain with no modifiers",
                    "effect":"a function that just returns it's argument unchanged"
                  },{
                    "id":"2",
                    "name":"forest",
                    "code":"f",
                    "description":"Forested terrain with +3 range defense, +1 melle defense",
                    "effect":"a function that takes a movement type and a cost and returns a new cost"
                  }
                ]
              }
            ],
            "turns": [
              {
                "id": "1",
                "name": "Turn 1",
                "number": 1,
                "introduction": "Your people are ready to explore the universe, good luck",
                "results":"",
                "positionActions":[
                ],
                "unitActions":[
                ]
              }
            ],
            "currentTurn":1,
            "status": "PREPARING",
            "nextTick": "2016-12-03T00:00:00.000Z",
            "users": [
              {
                "id":"1",
                "name": "Inspector Gadget",
                "role": "HOST"
              }, {
                "id":"2",
                "name": "Cortrah",
                "role": "PLAYER"
              }, {
                "id":"3",
                "name": "Kolgrim",
                "role": "PLAYER"
              }
            ]
          }
        }{
           "1": {
             "id": "1",
             "name": "Space Opera",
             "positions": [
               {
                 "id": "1",
                 "name": "Hyperion Flow",
                 "code": "hyp",
                 "userId":"2",
                 "color": "11223344",
                 "firstTurn":1,
                 "lastTurn":1,
                 "isSecret": false,
                 "regions":["1","2"],
                 "score":0,
                 "tradeValue":5,
                 "tradePartners":[],
                 "allies":[],
                 "money":100,
                 "materials":100,
                 "research":100,
                 "moneyIncome":10,
                 "materialIncome":10,
                 "researchIncome":10,
                 "units":[],
                 "items":[]
               },
               {
                 "id": "2",
                 "name": "AstroDog Pack",
                 "code": "hyp",
                 "userId":"3",
                 "color": "44332211",
                 "firstTurn":1,
                 "lastTurn":1,
                 "isSecret": false,
                 "regions":["3","4"],
                 "score":0,
                 "tradeValue":5,
                 "tradePartners":[],
                 "allies":[],
                 "money":100,
                 "materials":100,
                 "research":100,
                 "moneyIncome":10,
                 "materialIncome":10,
                 "researchIncome":10,
                 "units":[]
               }
             ],
             "maps": [
               {
                 "id": "1",
                 "name": "Galaxy Map",
                 "code": "gm",
                 "rows": 2,
                 "cols": 2,
                 "bg": "galaxy.png",
                 "regions": [
                   {
                     "id": "1",
                     "name": "Syrius",
                     "code": "sys",
                     "row": 1,
                     "col": 1,
                     "environmentTypeId": 1,
                     "borders":["1","2"],
                     "isSecret": false
                   },
                   {
                     "id": "2",
                     "name": "Speakeasy",
                     "code": "spk",
                     "row": 1,
                     "col": 2,
                     "environmentTypeId": 1,
                     "borders":["1","3"],
                     "isSecret": false
                   },
                   {
                     "id": "3",
                     "name": "Beelzebub",
                     "code": "bub",
                     "row": 2,
                     "col": 1,
                     "environmentTypeId": 1,
                     "borders":["2","4"],
                     "isSecret": false
                   },
                   {
                     "id": "4",
                     "name": "Frankenberry",
                     "code": "fby",
                     "row": 2,
                     "col": 2,
                     "environmentTypeId": 1,
                     "borders":["3","4"],
                     "isSecret": false
                   }
                 ],
                 "regionsBorders":[
                   {
                     "id":"1",
                     "name":"Syrius-Speakeasy",
                     "code":"1-2",
                     "sourceRegionId": "1",
                     "sinkRegionId": "2",
                     "borderTypeId": "1",
                     "isSecret": false
                   },{
                     "id":"2",
                     "name":"Syrius-Beelzebub",
                     "code":"1-3",
                     "sourceRegionId": "1",
                     "sinkRegionId": "3",
                     "borderTypeId": "1",
                     "isSecret": false
                   },          {
                     "id":"3",
                     "name":"SpeakEasy-Frankenberry",
                     "code":"2-4",
                     "sourceRegionId": "2",
                     "sinkRegionId": "4",
                     "borderTypeId": "1",
                     "isSecret": false
                   },{
                     "id":"4",
                     "name":"Beelzebub-Frankenberry",
                     "code":"3-4",
                     "sourceRegionId": "3",
                     "sinkRegionId": "4",
                     "borderTypeId": "1",
                     "isSecret": false
                   }
                 ],
                 "borderTypes":[{
                     "id": "1",
                     "name": "adjacent",
                     "code": "adj",
                     "description": "Allows unrestricted movement at no cost",
                     "isDirectional": "false"
                   }
                 ],
                 "environmentTypes":[
                   {
                     "id":"1",
                     "name":"clear",
                     "code":"c",
                     "description":"Basic flat terrain with no modifiers",
                     "effect":"a function that just returns it's argument unchanged"
                   },{
                     "id":"2",
                     "name":"forest",
                     "code":"f",
                     "description":"Forested terrain with +3 range defense, +1 melle defense",
                     "effect":"a function that takes a movement type and a cost and returns a new cost"
                   }
                 ]
               }
             ],
             "turns": [
               {
                 "id": "1",
                 "name": "Turn 1",
                 "number": 1,
                 "introduction": "Your people are ready to explore the universe, good luck",
                 "results":"",
                 "positionActions":[
                 ],
                 "unitActions":[
                 ]
               }
             ],
             "currentTurn":1,
             "status": "PREPARING",
             "nextTick": "2016-12-03T00:00:00.000Z",
             "users": [
               {
                 "id":"1",
                 "name": "Inspector Gadget",
                 "role": "HOST"
               }, {
                 "id":"2",
                 "name": "Cortrah",
                 "role": "PLAYER"
               }, {
                 "id":"3",
                 "name": "Kolgrim",
                 "role": "PLAYER"
               }
             ]
           }
         }