## D. Secure User Accounts

Allowing user accounts creates many complexities in our design. Let's try to create and integrate secure accounts for users into our database design. See the [`secure_accounts` branch of our demo code](https://github.com/ISS-Security/configshare/tree/3-secure_accounts).

1. Switching to SimpleBox to handle nonces
  - Change your migrations to remove the nonce columns from your tables
  - Update your security module (rename it `SecureModel`) to return `SimpleBox`'s ciphertext+nonce.
  - Update your models so they don't have to worry about nonces anymore!
2. User accounts: let's create/update accounts for our users
  - First, consider what to call your user accounts based on our class discussion
  - Create a migration/model for user accounts
  - Add a hashed password field to your user accounts:
    - Make sure your migrations add a hashed password field
    - Give `SecureModule` new functions to hash passwords as well
    - Give your user account model the ability to set and *check* (not get!) passwords
  - Consider any many-to-many relationships that arise in your database design
    - add any required many-to-many relationships in your models
    - create required *join tables*
    - use association_dependencies, before/after hooks to maintain table integrity
3. Create service objects to remove database code from controllers
  - Create service objects wherever you find you have to write several lines of code to get around mass assignment restrictions (e.g., on new/create of models)
  - Can you think of other places where we could extract code away from our controllers or models? Add Github issues with suggestions to clean up our code. We will spend some time discussing this before deploying our APIs into production.
4. Project structure cleanup
  - Breakup your `app.rb` into multiple controller files and move them into a `controllers/` subfolder
  - Create an `init.rb` in each of your subfolders where you have active code, and require those `init.rb` files whenever you need to load major parts of your application
5. Update your Github issues
  - Create Github Issues for any new vulnerabilities that you can think of
  - Close any previous issues that we have already solved (if you feel we haven't solved them, tell us why in class)
