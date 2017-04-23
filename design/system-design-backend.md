# system design

following these 4 steps can help you tackle any system design problem.

## example: design a calendar

1. scale
 - queries per second. Read? Write? Use harddisk or RAM?
 - does latency matter?
 - what features? (user register, can create event, book a conference room, etc)
 - what user interface? what platform?

2. service
 - user service (MySql)
   User
   userId userName email password registeredAt

 - calendar service (NoSql)
   Event
   eventId eventName startTime endTime users notes status

 - image, files storage: file system

 - user interface (client-side program)
   browser? mobile app?

3. storage
 - user service: mysql
 - calendar service:
 - image, files storage

4. functionality in detai
 - what api?
   - `query(user, day)`
    - `insert(user, event)` 
    - `delete(user, event)`
 - what's the structure of HTTP response?

## storage pros vs. cons

MySql
 1. schema must be maintained and kept in sync between application and database

 Good:
 - great for solutions where every record has the same structure
 - good for structured data
 - relationships are often captured in normalized models using joins
   to resolve references across tables
 - strong consistency

 Bad:
 - adding new property on table schema requires backfill


NoSql
 1. dynamic / flexible schema
 2. relationships are often captured by denormalizing data and
    presenting all data for an object in a single record

 Good
 - new properties can be added on the fly


Redis: NoSql database used for caching

