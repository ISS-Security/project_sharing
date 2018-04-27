## Database Hardening

Using a database solves many of our security problems and also introduces new problems. This week we will advance our database driven system by preventing common vulnerabilities and introducing encryption. See the `db_hardening` branch of our demo code.

1. Reshape your **project structure**
  - Move `app.rb` into a new `/controllers` folder
  - Create an `init.rb` in each major subfolder to load all Ruby files
  - Create a master `init.rb` in the root of your project to load subfolder `init.rb`s in order of least to most dependent (and call this from `config.ru` and elsewhere)
2. Prevent **mass assignment** vulnerabilities by restricting columns users can influence
  - Add a whitelist of permissible methods to restrict which attributes of your models can be changed by a mass assignment from user input
  - Add tests to ensure that mass assignment does not work (returns `400`)
3. Prevent **SQL injection** attacks
  - Use string literalization and/or query parameterization
4. **UUID**s _(optional)_
  - Discuss with your team if there are any primary keys that should be UUIDs
  - Modify the migrations and models for those tables to use UUIDs
    - Use a `uuid` type in your migrations
    - Use the `:uuid` plugin in models to autogenerate UUIDs
5. **Encrypt** any sensitive columns that should not be read if your database is stolen
  - Discuss with your team which columns of which tables contain the most sensitive data
  - Create a `SecureDB` class to encrypt/decrypt and other methods
    - Put the new class in a new `lib/` folder
    - Use `rbnacl/libsodium`'s `Simplebox` to encrypt/decrypt
    - Inject EConfig's `config` object into your `SecureDB` class at app startup
    - (optional) create a `Rake` task to generate database keys for you at command line
  - Use the `econfig` gem to load a database key from `config/secrets.yml`
    - ⚠️ Don't forget to put your configuration file in `.gitignore`!
    - Create a database key for your `development` and `test` environments only for now
  - Encrypt!
    - Change the name of encrypted columns (with a prefix/suffix like `secure_`)
    - Create getter and setter methods in your models to encrypt/decrypt columns in memory
6. Update your Github issues
  - Create Github Issues for any new vulnerabilities that you can think of
  - Close any previous issues that we have already solved (if you feel we haven't solved them, tell us why in class)
