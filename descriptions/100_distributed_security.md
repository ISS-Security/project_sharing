# Distributed Security: Signed Clients and XSS Prevention

Our last security tasks of the semester is to help our API trust our client Application, and to ask the user's browser to help prevent cross-site scripting and code injection.

Relevant code branches for App and API:
- App: [8-xss_protection](https://github.com/ISS-Security/configshare-app/tree/8-xss_protection)
- API: [8-authorize_client_app](https://github.com/ISS-Security/configshare/tree/8-authorize_client_app)

1. Signed Client - API Routes that cannot have an auth_token must only accept signed requests
  - Examples of routes in the demonstration Config-Share API:
    - `POST '/api/v1/accounts`
    - `POST '/api/v1/accounts/authenticate`
    - `GET '/api/v1/github_account`
  - Create `Ed25519` public and secret keys for your Application
    - You might find it helpful to create a Rake task that generates asymmetric keys for you
    - Store your App's secret key in its `config_env.rb`
    - Store your App's public key in the API's `config_env.rb`
  - Create helper methods in your App and API to sign and verify messages, respectively
    - Create a `def self.sign` method in your App's SecureMessage (or similar) library
    - Create a `def self.verify` method in your API's SecureMessage (or similar) library
  - Modify the relevant service objects of your App and API to sign/verify requests
    - note: you should not have any API calls in your controllers
2. Preventing XSS
  - See our in-class [demo code for launching and preventing XSS attacks](https://github.com/ISS-Security/demo-xss)
  - clone the demo code and make sure it works on your machine:
    - comment out the protection code at the bottom of `app.rb` to allow exploiting XSS
    - remove commenting and allow XSS protection to see that it catches code injection
  - copy and modify this protection code to your App
    - consider making a security controller that enables all these settings
3. Implement all remaining functionality of your application and API:
  - Accounts must be able to create all relevant resources
  - Accounts must be able to share resources between each other where appropriate
