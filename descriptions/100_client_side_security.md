# Client-side Security: Signed Clients and XSS Prevention

Our last security tasks of the semester is to help our API trust our client Application, and to ask the user's browser to help prevent cross-site scripting and code injection.

Relevant code branches for App and API:
- Web App: [signed_protected](https://github.com/ISS-Security/configshare-app/tree/6_signed_protected)
- Web API: [signed_requests](https://github.com/ISS-Security/configshare-api/tree/8_signed_requests)

1. Signed Client - API Routes that cannot have an auth_token must only accept signed requests
  - Update your `SecureMessage` library to sign messages
  - At a minimum, all POST requests to API that cannot provide an `auth_token` must be signed
  - Send your signed json requests with separate `data` and `signature` parts
2. Preventing XSS/CSRF
  - See our in-class [demo code for launching and preventing XSS attacks](https://github.com/ISS-Security/demo-xss)
  - clone the demo code and make sure it works on your machine:
    - comment out the protection code in the second half of `app.rb` to allow exploiting XSS/CSRF
    - remove commenting and allow XSS protection to see that it catches code injection
  - copy and modify this protection code to your App
    - make a security controller file that enables all these settings (e.g., `/controllers/security.rb`)
    - make sure security controller is loaded before `/controllers/base.rb`
3. Implement all remaining functionality of your application and API:
  - Accounts must be able to create all relevant resources
  - Accounts must be able to share resources between each other where appropriate
