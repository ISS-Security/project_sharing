## Database Hardening

Using a database solves many of our security problems and also introduces new problems. This week we will advance our database driven system by preventing common vulnerabilities and introducing encryption. See the [`db_hardening` branch of our demo code](https://github.com/ISS-Security/configshare-api/tree/2_db_hardening).

1. Reshape your project structure
  - Break your app.rb into many smaller files under `/controllers`
    - Make a `./controllers/base.rb`
    - Reopen your Sinatra class in subfolders/files within controllers
    - Ensure that each major route (e.g. `api/v1/projects`) has its own subfolder and controller files (e.g., `./controllers/projects/projects.rb`)
  - Create an `init.rb` in each major subfolder to load all Ruby files
  - Create an `./init.rb` in the root of your project to load a subfolder `init.rb`s in order of least to most dependent (and call this from `config.ru` and `specs/spec_helper.rb`)
2. Prevent mass assignment vulnerabilities by restricting columns users can influence
  - Add a `set_allowed_columns` method we saw in class to restrict which attributes of your models can be changed by a mass assignment from user input
  - Discuss with your teammates whether the encrypted fields you will create this week can be mass assigned or not
3. Prevent SQL injection attacks by using literalization and query parameterization
  - Identify all routes where you might manually be creating SQL queries
  - At least use literalization to resolve all queries
  - You may optionally also use query parameterization (bound statements) to create a SQL query that does not contain any values.
4. UUIDs (optional)
  - Discuss with your team if there are any primary keys that should be UUIDs
    - be prepared to justify your reasoning in class
    - tell us how sequential IDs or other guessable attributes could be exploited
  - modify the migrations and models for those tables to use UUIDs
    - use the `:uuid` plugin to implement UUIDs
    - make sure your tests still pass!
5. Encrypt any sensitive columns that should not be read if your database is stolen
  - Discuss with your team which columns of which tables contain the most sensitive data
  - Encrypt just those sensitive columns
    - Use the `econfig` gem to create a configuration file `./config/app.yml` to store your database key
      - don't forget to put your configuration file in `.gitignore`!
      - create a database key for your `development` and `test` environments only for now
    - Create a `SecureDB` class in `./lib/secure_db.rb` to create encrypt/decrypt and other methods
      - Use `rbnacl/libsodium`'s `Simplebox` to encrypt/decrypt
      - Inject Sinatra's `config` into your `SecureDB` class at app startup
      - (optional) create a `Rake` task to generate keys for you at command line
6. Update your Github issues
  - Create Github Issues for any new vulnerabilities that you can think of
  - Close any previous issues that we have already solved (if you feel we haven't solved them, tell us why in class)
