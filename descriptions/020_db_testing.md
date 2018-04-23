## Relational Database and ORM

We will start addressing some of the security issues we found by adding a database to our application and writing tests for it. You can refer to the `1_db_orm` branch of the demo code we saw in class.

Before you Start: a short video introduction to the `Sequel` gem from a coding master:
[Sequel Introduction Video](https://www.rubytapas.com/2014/02/20/episode-179-sequel/)

1. Write migrations to create relational tables for your project
  - Identify *at least two tables* you will need for your project, except for a user table
  - Add gems to `Gemfile` and `config/environments.rb` as we saw in class
  - Create migration files in `db/migrations/` to create your tables
  - Create a `Rakefile` with a `db:migrate` task
  - Create `db/dev.db` and `db/test.db` Sqlite databases for the development and test environments using your migrations
  - Add `db/*.*` to your `.gitignore` to ignore the databases, but not your migrations
  - Be careful to follow the plural/singular conventions of Sequel
  - Resources
    - [Sequel Migrations: Introduction](http://sequel.jeremyevans.net/rdoc/files/doc/migration_rdoc.html)
    - [Sequel Migrations: Schema Modification](http://sequel.jeremyevans.net/rdoc/files/doc/schema_modification_rdoc.html)
    - [Sequel Migrations: Timestamps](http://sequel.jeremyevans.net/rdoc-plugins/classes/Sequel/Plugins/Timestamps.html)
2. Create models and play with your new database!
  - Create new `Sequel` based model classes in `models/`, with appropriate associations
  - Be careful to follow the plural/singular conventions of Sequel
  - Integrate your models in your application:
    - require `config/environments.rb` in `app.rb`
    - you can create a `models/init.rb` that requires all the models, and then include this `init.rb` in your `app.rb`
  - Create and use a `console` task in Rakefile that launches `pry` with all your code preloaded. You can use it see if you can add/update/delete records across your tables
  - You an use the `Hirb` gem to see tabular views of your records within `rake console`
  - Resources
    - [Sequel Models: Associations](http://sequel.jeremyevans.net/rdoc/files/doc/association_basics_rdoc.html)
    - [Sequel Queries](http://sequel.jeremyevans.net/rdoc/files/doc/querying_rdoc.html)
    - [Sequel Filters](http://sequel.jeremyevans.net/rdoc/files/doc/dataset_filtering_rdoc.html)
3. Update your routes and test them!
  - Try to write tests for each route *before* you write the code for that route
    - Test the root route of your Web API to make sure it returns a valid message
    - Test each GET and POST route you create
      - Add a `before` block to your tests that deletes your tables before each test!
      - Write a 'happy' path that tests a successful case for each route
      - Write *at least one* 'sad' path that tests a fail case for each route
  - Update your old routes from last week and add new ones where necessary
    - add more GET routes to get indexes and individual resources
    - add POST routes to create each resource in your database
4. What are some new security risks we might have introduced this week?
  - Update your Github issues for these vulnerabilities that you can think of
  - Have we resolved any issues from last week? Let us know by closing any previous issues!
