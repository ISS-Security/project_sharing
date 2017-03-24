# F. Token Based Authentication

This week we will use tokens (JWT) in our authentication process. You'll see that tokens allow us to securely store information about the state of the session on the client's side. See the latest version of our [application side code](https://github.com/ISS-Security/configshare-app/tree/2-token_authentication).

1. Create a secure messaging library for all outgoing messages
  - Create a class in `/lib` that can encrypt and decrypt any message
  - Use the `jose` gem to handle cryptography using secure JWT
2. Use encrypted JWT for account information cookies
  - Use your secure messaging library to encrypt cookies before sending them
  - Decrypt cookies in a `before` block of your Sinatra application
3. Create a registration workflow that verifies user emails
  - Allow users to create accounts with only username and email
  - Verify the email address by sending an email
    - Use Pony + Sendgrid to send the verification email with a link back to our site
    - Use your secure messaging library to create an encrypted JWT token to embed (username + email) in the link
  - Once users return using their verification link, ask for password + password confirmation
  - Create users who have finished the entire process (use a service object)
