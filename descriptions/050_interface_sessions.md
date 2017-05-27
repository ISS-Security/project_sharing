# Client Interface and Sessions

This week are building up our interface as a web client application. We are interested in seeing if we can get users to login for now! Take a look at the latest code at:
  - [Deployed API](https://github.com/ISS-Security/configshare-api/tree/4_authenticate_accounts)
  - [Interface Client](https://github.com/ISS-Security/configshare-app/tree/1_login_session)

1. Updating our API Structure
  - Try to see if all your API routes can use service objects
    - Only do parameter parsing in your controller, and then call a service object
    - After you have created many service objects, your `services/` folder should give a good idea of what your project does
  - Add a POST route to your API to authenticate credentials `post '/api/v1/accounts/authenticate'`
    - If username/password is correct, return JSONified user information
    - Otherwise, return a 403 error code
2. Create a simple client interface application
  - Create controllers, services, and Slim views for:
    - a layout template with navigation bar (home/login/register or home/account/logout)
    - a home page
    - a login page
    - an account overview page for logged in users
  - Allow users to login using the login page
    - Use a service object call to authenticate the user with your API
    - Use a cookie to store the logged in user's username and other information
  - Allow users to logout by destroying their cookie and any objects with their information
  - Allow logged in users to see their account information
3. Add flash messages for errors and notices
  - Use the `rack-flash3` gem to create flash messages
  - Add a flash message bar to your `layout.slim`
  - Create CSS file in `/public` folder for `:error` and `:notice` styles
    - Set the location of your public directory for Sinatra
  - Provide flash notices for form errors and important transitions (e.g., logout)
4. Enforce SSL connections
  - Use the `rack-ssl-enforcer` gem to enforce SSL connections on *production* servers (won't work during development/testing)
  - Enforce SSL for both your API and your web application
5. Examine the security of your solution so far
  - Create Github issues for what security weaknesses our interface / API face
  - Close any old issues that have been resolved now
