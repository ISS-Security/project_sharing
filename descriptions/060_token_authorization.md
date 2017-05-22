# Token Based Authentication

This week we will introduce authorization to our system, using authorization tokens. See the latest version of our demo project:
- [Web API: authorized_access](https://github.com/ISS-Security/configshare-api/tree/5_auth_token)
- [Web App: authorized_access](https://github.com/ISS-Security/configshare-app/tree/3_auth_token)

1. Create a secure library to handle authorization tokens
  - Create an `AuthToken` LIBRARY:
    - We will need to reuse some security code from our `SecureDB` library
      - Refactor `SecureDB` to extract a `Securable` module that handles all the crypto logic
      - Both `SecureDB` and `AuthToken` should extend `Securable`
    - Make sure you have some methods to `create` tokens and extract `payload` from tokens
    - Make sure `AuthToken` throws errors for expired tokens and invalid tokens
    - I suggest making a unit test to make sure `AuthToken` handles all happy, sad, and bad cases

2. Web API: Issue and require auth tokens
  - Send back an auth token (encrypted account information) along with raw account information whenever an account is authenticated
  - Whenever a route requires accessing an account's resources, check the auth token
    - Create helper methods that verify identify of account identity of token with resource owner
      - Check token in `HTTP_AUTHENTICATION` header of HTTP request as `'Bearer <TOKEN>'`
    - Return error 401 for any suspicious cases:
      - if token is expired
      - if identify of owner in auth token does not match route
      - if resource does not belong to account in auth token

3. Web App: Store and use auth tokens
  - Store auth tokens safely as session information (secure it using `SecureSession`)
  - Return API's auth token on every request
    - Send auth token to API in every request as `HTTP_AUTHENTICATION` header: `'Bearer <TOKEN>'`
    - Allow users to see their own token in their account page

4. API+App: Add features in App to view all resources
  - Ensure your API not only allows for authentication, but can now create/find one or more resources that belong to accounts
  - Ensure that your Web App has views to create/retrieve resources
  - Users can see their account information
  - Users can see all resources they own
  - Users can see all resources they are shared with others
