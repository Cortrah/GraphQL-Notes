# GraphQL Notes

These are some notes about graphql in preparation for doing a presentation.

### The value from a client side perspective

* The process of getting new end points and data being dependent on others schedules
* Flexibility
* Efficiency
* Maintenance
* Living Documentation

### Potential Problems
* security
* complexity
* keeping the hot side hot and the cold side cold
* strong typing without strong tooling

### Related Predecessors
* Odata with breeze and jaydata  
* Breeze schemas entity framework and hand entering metadata 
* Rest, JsonApi specifically (article on discrourse)
* HATEOS, RPC, SOAP - remember the past to predict the future - SOAP stories?
  
  
### Features
* getting data with different structures 
* sorting 
* paging 
* validation 
* caching
  
The syntax is a query language using the best part of js, json

So it looks like json, until it doesn't
  
A visual/aural dictionary of terms on mouseover of a good example query. Go through each term in the spec
  
### Creating schemas will be the challenge as it is with breeze

It is a strongly tyhped system that is based on js making it strange to many of it's target users

Examples of mapping to
* mongo via mongoose, joi or json schema
* postgres with sequelize or absynthe
* Ruby
* Elixir
  
Apollo and the state of various projects, activity, moving quick, but lots of fits and starts as well. Blog summary? Any Predictions?

ok now back to the syntax, with authorizaqtion, authentication, parameterization

### Testing

types of testing, schema, unit, query, edge cases, validation, end to end, 

### Some ideas for an example

1. An oddworks video catelog using CQRS using a range tree to implement a suggestion feature for policy wonks scanning through commercials on msnbc or cspan by monitoring fast forwarding and rewinding to hone in on interesting content.

2. a map drawing tool with express and react dnd

3. a text based schema building interface that could map to languages and back ends using span/selector mad libs with natural language

4. absynthe to ember or aurelia using fragment types mapped to templates

5. joint.js schema building interface instead of span based text markup for phones. envisioning refactoring tools with handle and fragment types

6. use DDD tool dictionary to easitly or auto populate names as an option for phone based sketching

7. Hapi based schema editor using joi

If I do the tool, some fun implementation ideas
* Squee like mee byron mascot in a spacesuit in an Apollo craft, worried, debree outside
* SqueeMe is the tool
* SqueeMish is the schema file format
* .squish is the file extension

If I do an absynthe example, cover
* LINQ to SQL Server
* ECTO to Postgres
* Execution plans and querying strategy good practices

### A Schema to Experiment with for a Board Game Map

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