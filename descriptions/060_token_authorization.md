# Token Based Authentication

This week we will introduce email verification and token-based authorization to our system.

1. Create a registration workflow that verifies user emails
- Allow users to create accounts with only username and email
- Verify the email address by sending an email from the API
  - Use SendGrid API (or gem) to send the verification email with a link back to our site
  - Use your App's secure messaging library to create an encrypted token containing username/email
  - Link should contain URL to Web application (not API)
- Once users return using their verification link, ask for password + password confirmation
- Create users who have finished the entire process

2. Web API: Create a secure library to manage authorization tokens
- Create an `AuthToken` library:
  - We will need to reuse some security code from our `SecureDB` library
    - Refactor `SecureDB` to extract a `Securable` module that handles all the crypto logic
    - Both `SecureDB` and `AuthToken` should extend `Securable`
  - Make sure you have some methods to `create` tokens and extract `payload` from tokens
  - Make sure `AuthToken` throws errors for expired tokens and invalid tokens
  - I suggest making a unit test to make sure `AuthToken` handles all happy, sad, and bad cases

3. Web API: Issue and require auth tokens
- Send back an auth token (encrypted account information) along with raw account information whenever an account is authenticated
- Whenever a route requires accessing an account's resources, check the auth token
  - Create helper methods that verify identify of account identity of token with resource owner
    - Check token in `HTTP_AUTHENTICATION` header of HTTP request has `'Bearer <TOKEN>'`
  - Return error 401 for any suspicious cases:
    - if token is expired
    - if identify of owner in auth token does not match route
    - if resource does not belong to account in auth token

4. Web App: Store and use auth tokens
- Store auth tokens safely as session information (secure it using `SecureSession`)
- Send auth token to API in every request as `HTTP_AUTHENTICATION` header: `'Bearer <TOKEN>'`

5. API+App: Add features in App to view index of resources
- Users can see all resources they own
- Users can see all resources they are shared with others
