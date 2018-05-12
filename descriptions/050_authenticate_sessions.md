# Client Interface and Sessions

This week are building up our interface as a web client application. We are interested in seeing if we can get users to login for now! Take a look at the latest demo code online.

## Web API
1. Updating our API Structure
  - Split your controller into multiple files
  - Use the `multi_route` plugin for Roda
2. Add POST route to API to authenticate credentials
    - e.g., `post '/api/v1/accounts/authenticate'`
    - If username/password is correct, return JSONified user information
    - Otherwise, return a 403 error code with a json message body
3. Require SSL connections to API
  - Check protocol schema for incoming requests
  - Block non-secure requests for production (HTTP)

## Web App
1. Create a simple client interface application
  - Create controllers, services, and Slim views for:
    - a layout template with navigation bar (home/login/register or home/account/logout)
    - a home page
    - a login page
    - an account overview page for logged in users
  - Allow users to login using the login page
    - Use a service object call to authenticate the user with your API
    - Use a cookie to store the logged in user's username and other non-sensitive information
  - Allow logged in users to see their account information on an accounts page
  - Allow users to logout by deleting account information from cookie
2. Add flash messages for errors and notices
  - Use the `rack-flash3` gem to create flash messages
  - Add a flash message bar to your `layout.slim`
  - Create CSS file in `/public` folder for `:error` and `:notice` styles
    - Set the location of your public directory for Sinatra
  - Provide flash notices for form errors and important transitions (e.g., logout)

Examine the security of your solution so far:
  - Create Github issues for what security weaknesses our interface / API face
  - Close any old issues that have been resolved now
