## B. Database and Testing

We will start addressing some of the security issues we found by adding a database to our application and writing tests for it. You can refer to the [`db_testing` branch of the demo code we saw in class](https://github.com/ISS-Security/configshare/tree/1_db_testing).

Before you Start: a short video introduction to migrations, models, and filters of the `Sequel` gem
  - [Sequel Introduction Video](http://www.rubytapas.com/episodes/179-Sequel)


1. Write migrations to create relational tables for your project
  - Discuss with your team what tables you might need for your project, moving forward
  - add gems to `Gemfile` and `config/environments.rb` as we saw in class
  - Create a `db/migrations` folder and put migration files in it
  - Create a `Rakefile` with `db:migration` and `db:reset` tasks
  - Create `db/dev.db` and `db/test.db` Sqlite databases for the development and test environments
  - Resources
    - [Sequel Migrations: Introduction](http://sequel.jeremyevans.net/rdoc/files/doc/migration_rdoc.html)
    - [Sequel Migrations: Schema Modification](http://sequel.jeremyevans.net/rdoc/files/doc/schema_modification_rdoc.html)
    - [Sequel Migrations: Timestamps](http://sequel.jeremyevans.net/rdoc-plugins/classes/Sequel/Plugins/Timestamps.html)
2. Create Models and play with your new database!
  - Update and create new model classes in your `models/` folder
  - Integrate your models in your application:
    - require `environments.rb` in `app.rb`
    - you can create a `models/init.rb` that requires all the models, and then include this `init.rb` in your app
  - Run the `tux` gem from the command line and see if you can add/update/delete records from your tables
  - Resources
    - [Sequel Models: Associations](http://sequel.jeremyevans.net/rdoc/files/doc/association_basics_rdoc.html)
    - [Sequel Queries](http://sequel.jeremyevans.net/rdoc/files/doc/querying_rdoc.html)
    - [Sequel Filters](http://sequel.jeremyevans.net/rdoc/files/doc/dataset_filtering_rdoc.html)
3. Update your routes and test them!
  - Update all your routes from last week and add new ones where necessary
    - add more GET routes to get indexes and resources
    - add POST routes to create resources in your database!
  - Write tests for each route *before* your write the code for that route
    - Test the root route of your Web API to make sure it returns a valid message
    - Test each GET and POST route you create
      - Write a 'happy' path that tests a successful case for each route
      - Write at least one 'sad' path that tests a fail case for each route
      - Add a `before` block to your tests that deletes your tables before each test!
4. What are some new security risks we might have introduced this week?
  - Create Github Issues for these vulnerabilities that you can think of
  - Have we resolved any issues from last week? Let us know by closing any previous issues!
