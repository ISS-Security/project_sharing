# Token Based Authorization

This week will implement the beginnings of authorization, and we will use tokens once again. Note that all the critical authorization decisions will be done on the API side. Thus, the API must create and send an encrypted token that must be returned by client applications on every request.

For example code, take a look at the following branches of the API and App:
- [API: authorized_access](https://github.com/ISS-Security/configshare/tree/5-authorized_access)
- [App: authorized_access](https://github.com/ISS-Security/configshare-app/tree/4-authorized_access)

1. API: Send and Require an Authentication Token from Client Apps
  - Create `JWE` or such library class to encrypt/decrypt JWT tokens for API
  - Return an encrypted token when client applications authenticate credentials (username, password)
    - Change API authentication route:
      - use POST instead of GET
      - require authentication credentials as json in HTTP body instead of URL parameters
      - make authentication route something like: `/api/v1/accounts/authenticate`
    - Return:
      - regular a account information (`id`, `username`, `password`) for the application
      - an encrypted JWT that only the API can decrypt in future (expire after a week or so)
  - Check authentication token on each data related request
    - Create helper methods that verify identify of account identity of token with resource owner
      - Check token in `HTTP_AUTHENTICATION` header of HTTP request as `'Bearer <TOKEN>'`
    - Return error 401 for any suspicious cases:
      - if token is expired
      - if identify of owner in `auth_token` does not match route
      - if resource does not belong to account in `auth_token`
2. App: Return API's `auth_token` on every request
  - Store API `auth_token` in user session cookie along with regular account information
  - Send `auth_token` to API in every request as `HTTP_AUTHENTICATION` header: `'Bearer <TOKEN>'`
  - Allow users to see their own token in their account page
3. API+App: Add features
  - Add features in App to view all resources:
    - Users can see their account information
    - Users can see all resources they own
    - Users can see all resources they are sharing with others
  - Make sure all new API routes you need use token based authorization
