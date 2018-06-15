# Client-side Security: Signed Clients and XSS/CSRF Prevention

Our last security tasks of the semester is to help our API trust our client Application, and to ask direct the user's browser to help prevent cross-site scripting, code injection, and cross-site resource forgery.

## 1. App: Signed Client - API Routes that cannot have an auth_token must only accept signed requests

- API: Require signed routes
  - At a minimum, all POST requests to API that cannot provide an `auth_token` must be signed
  - Create a `SignedRequest` library to verify signed requests using a verify key
  - Relevant controllers should verify signed requests before passing parsed data to service objects
- App: Sign critical requests:
  - Update your `SecureMessage` library to sign messages using a signing key the API has created
  - Send your signed json requests with separate `data` and `signature` parts

## 2. Preventing XSS/CSRF/code-injection and forged assets

- Send security directives to browser:
  - Make a security controller file that enables all these settings (e.g., `/controllers/security.rb`)
  - Move all security related code from `/config/environments.rb` to the new security controller
  - Add secure headers to protect cookies, default browser behaviors, and content security policies
  - Add a reporting route that the browser can report CSP violations to
- Ensure all third party scripts, stylesheets, fonts, and other assets have an integrity hash for browsers to check

## 3. Implement all remaining functionality of your application and API

- Accounts must be able to create all relevant resources
- Accounts must be able to share resources between each other where appropriate
