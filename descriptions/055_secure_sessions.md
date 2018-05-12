# Secure Sessions and Registration

This week we will secure the storage of session state across our system and on the client machine. See the latest version of our demo code.

1. Let's update some of the security choices we made last week
  - Try adding tests for the web application's service objects: *stub* any outward HTTP requests to the API
  - If you are using cookies for any non-session purposes, make sure to implement a strong session secret nonce
1. Enforce SSL connections for Web App
  - Use the `rack-ssl-enforcer` gem to enforce SSL connections on *production* servers (won't work during development/testing)
  - Redirect users to secure HTTPS connections
2. Let's switch our session storage to server-side pool
  - Provision a Redis machine on Heroku
  - Specify Redis as our application's session store
3. Use encrypted session variables
  - Create a secure messaging library for all outgoing messages
    - Create a class in `/lib` that can `encrypt` and `decrypt` any message
    - it should be able to `encrypt` and `decrypt` any message using a secret `MSG_KEY`
  - Create a secure session library
    - Create a class in `/lib` that can securely `set` and `get` session variables
    - Use the NaCl library (`rbnacl/libsodium`) for all cryptography
3. Create a registration workflow that verifies user emails
  - Allow users to create accounts with only username and email
  - Verify the email address by sending an email
    - Use Pony + SendGrid to send the verification email with a link back to our site
    - Use your secure messaging library to create an encrypted token to embed the new account information in the link
  - Once users return using their verification link, ask for password + password confirmation
  - Create users who have finished the entire process (use a service object)
