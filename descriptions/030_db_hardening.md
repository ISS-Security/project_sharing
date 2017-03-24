## C. Database Hardening

Using a database solves many of our security problems and also introduces new problems. This week we will advance our database driven system by preventing common vulnerabilities and introducing encryption. See the [`db_hardening` branch of our demo code](https://github.com/ISS-Security/configshare/tree/2-db_hardening).

1. Prevent mass assignment vulnerabilities by restricting columns users can influence
  - Add a `set_allowed_columns` method we saw in class to restrict which attributes of your models can be changed by a mass assignment from user input
  - Discuss with your teammates whether the encrypted fields you will create this week can be mass assigned or not
2. Prevent SQL injection attacks by using literalization and query parameterization
  - Identify all routes where you might manually be creating SQL queries
  - At least use literalization to resolve all queries
  - Find at least one place where you will use query parameterization (bound statements) to create a SQL query that does not contain any values.
3. UUIDs (optional)
  - Discuss with your team if there are any primary keys that should be UUIDs
    - be prepared to justify your reasoning in class
    - tell us how sequential IDs or other guessable attributes could be exploited
  - modify the migrations and models for those tables to use UUIDs
    - use the `:uuid` plugin to implement UUIDs
    - make sure your tests still pass!
4. Encrypt any sensitive columns that should not be read if your database is stolen
  - Discuss with your team which columns of which tables contain the most sensitive data
  - Encrypt just those sensitive columns
    - Use the `config_env` gem to create a configuration file to store your database key
      - don't forget to put your configuration file in `.gitignore`!
      - create a database key for your `development` and `test` environments only for now
    - Use `rbnacl/libsodium`'s `SecretBox` to encrypt sensitive fields
      - use the database key that `config_env` put into your environment variables
      - use a nonce to harden our encryption
        - *important:* never reuse a row's nonce! update it on each encryption
        (nonces prevent the same information in different rows from being encrypted into the same ciphertext)
        - remember: nonces are not meant to be secret; store them with your record
      - mixin encryption methods using an `EncryptableModel` module for those models
4. Update your Github issues
  - Create Github Issues for any new vulnerabilities that you can think of
  - Close any previous issues that we have already solved (if you feel we haven't solved them, tell us why in class)
