## Database and Testing

We will start addressing some of the security issues we found by adding a database to our application and writing tests for it. You can refer to the [`1_db_testing` branch of the demo code we saw in class](https://github.com/ISS-Security/configshare-api/tree/1_db_testing).

Before you Start: a short video introduction to the `Sequel` gem
  - [Sequel Introduction Video](https://www.rubytapas.com/2014/02/20/episode-179-sequel/)

0. Start tracking dependency updates
  - Everyone on your team should create an account on Gemnasium (gemnasium.com)
  - Add your team's API repo to Gemnasium (gemnasium.com) for dependency monitoring
  - [Add a Gemnasium badge](http://support.gemnasium.com/knowledgebase/articles/560841-how-to-add-the-gemnasiun-badge-to-my-project-readm) to your repo's README (which you should also update every week)
1. Write migrations to create relational tables for your project
  - Identify *at least two tables* you will need for your project, except for a user table
  - Add gems to `Gemfile` and `config/environments.rb` as we saw in class
  - Create migration files in `db/migrations/` to create your tables
  - Create a `Rakefile` with `db:migration` and `db:reset` tasks
  - Create `db/dev.db` and `db/test.db` Sqlite databases for the development and test environments
  - Add `db/*.*` to your `.gitignore` to ignore the databases, but not your migrations
  - Be careful to follow the plural/singular conventions of Sequel
  - Resources
    - [Sequel Migrations: Introduction](http://sequel.jeremyevans.net/rdoc/files/doc/migration_rdoc.html)
    - [Sequel Migrations: Schema Modification](http://sequel.jeremyevans.net/rdoc/files/doc/schema_modification_rdoc.html)
    - [Sequel Migrations: Timestamps](http://sequel.jeremyevans.net/rdoc-plugins/classes/Sequel/Plugins/Timestamps.html)
2. Create Models and play with your new database!
  - Create new `Sequel` based model classes in `models/`, with appropriate associations
  - Be careful to follow the plural/singular conventions of Sequel
  - Integrate your models in your application:
    - require `config/environments.rb` in `app.rb`
    - you can create a `models/init.rb` that requires all the models, and then include this `init.rb` in your `app.rb`
  - Run the `tux` gem from the command line and see if you can add/update/delete records across your tables
  - Resources
    - [Sequel Models: Associations](http://sequel.jeremyevans.net/rdoc/files/doc/association_basics_rdoc.html)
    - [Sequel Queries](http://sequel.jeremyevans.net/rdoc/files/doc/querying_rdoc.html)
    - [Sequel Filters](http://sequel.jeremyevans.net/rdoc/files/doc/dataset_filtering_rdoc.html)
3. Update your routes and test them!
  - Update all your routes from last week and add new ones where necessary
    - add more GET routes to get indexes and individual resources
    - add POST routes to create each resource in your database
  - Try to write tests for each route *before* you write the code for that route
    - Test the root route of your Web API to make sure it returns a valid message
    - Test each GET and POST route you create
      - Add a `before` block to your tests that deletes your tables before each test!
      - Write a 'happy' path that tests a successful case for each route
      - Write *at least one* 'sad' path that tests a fail case for each route
4. What are some new security risks we might have introduced this week?
  - Update your Github issues for these vulnerabilities that you can think of
  - Have we resolved any issues from last week? Let us know by closing any previous issues!
