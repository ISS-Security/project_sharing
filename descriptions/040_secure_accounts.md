## Secure User Accounts

Allowing user accounts creates many complexities in our design. Let's try to create and integrate secure accounts for users into our database design. See the [`secure_accounts` branch of our demo code](https://github.com/ISS-Security/configshare-api/tree/3_secure_accounts).

1. User accounts: let's create/update accounts for users
  - Create a migration and model (call it `Account`) for user accounts
  - Implement salted, hashed passwords using key stretching
    - Make sure your migrations add a hashed password field
    - Give your `SecureDB` library a `new_salt` and `hash_password` methods
    - Use either `scrypt` or `argon2` hashing from the `rbnacl` package
    - Give your user account model methods to set and *check* (not get!) passwords
2. Many-to-Many Associations
  - add any many-to-many relationships you need using *join tables*
  - create relationships in in both directions
  - name your relationships approrpiately in each direction
    (e.g., `collaborators` vs. `collaborations`)
  - use association_dependencies to maintain table integrity (use `destroy` or `nullify` to specify how to propagate resource destruction)
3. Use service objects to cleanup controllers and reuse functionality
  - Create service objects wherever you find you have to write chained methods multiple lines to create or change resources
  - Reuse your service objects in controlers, tests, seeding
4. Implement a database seeding task
  - Use the `sequel-seed` gem to create a `rake db:seed` task for your API
  - Put your seeding code in `seeds/<date>_<description>.rb` files (example, `20180503_create_all.rb`)
  - Ensure your code is run in a `run` method in a `Sequel.seed(:development)` call
  - Make sure that anyone who wants to collaborate with your team can get setup by simply using:
  ```
  bundle install
  rake db:migrate
  rake db:seed
  ```
5. Deploy your API to the cloud
  - Each team member:
    - Create a Heroku account for each team member
    - Add your SSH public key to your account
    - Install [Heroku command line tools](https://devcenter.heroku.com/articles/heroku-cli): this gives you a command line `heroku` command
  - Use `heroku` command to create a domain name for your API (e.g., `configshare-api`)
  - Put necessary environment variables on Heroku project settings
  - Bundle the `pg` gem for production only (put the `.bundle/` folder in `.gitignore`)
  - Ask Heroku to add a PostgreSql server for your API
  - Push your API's master branch to Heroku to deploy it, and migrate your database
  - Check if your API is publicly available online!
  - Add all teammates as collaborators to this project

 Lastly, update your Github issues
  - Create Github Issues for any new vulnerabilities that you can think of
  - Close any previous issues that we have already solved (if you feel we haven't solved them, tell us why in class)
