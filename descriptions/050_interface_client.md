# E. Deployed API and Interface Client

This week are are deploying our APIs into live production and building up our interface as a web client application. We are interested in seeing if we can get users to login for now! Take a look at the latest code at:
  - [Deployed API](https://github.com/ISS-Security/configshare)
  - [Interface Client](https://github.com/ISS-Security/configshare-app)

1. Updating our API Structure
  - Organizing our crypto code
    - After using SimpleBox, your mixed in crypto module should no longer need to access attributes of your model; it can become a separate library.
    - Try creating a `SecureDB` class in a new `lib/` folder
    - This new class can implement encrypt, decrypt, and salting functions (see example API project)
  - Try to see if all your API routes can use service objects
    - Only do parameter parsing in your controller, and then call a service object
    - After you have created many service objects, your `services/` folder should give a good idea of what your project does
  - Add a route for users to be authenticated: `/api/v1/<username>/authenticate?password=<password>`
    - If username/password is correct, return JSONified user information
    - Otherwise, return a 401 error code
2. Deploy your API
  - Install Heroku toolbelt on your local machine: this gives you a command line `heroku` command
  - Use `heroku` command to create a domain name for your API (e.g., `configshare-api`)
  - Put your environment variables on Heroku using one of the methods described in class
  - Bundle the `pg` gem for production only (put the `.bundle/` folder in `.gitignore`)
  - Ask Heroku to add a PostgreSql server for your API
  - Push your API's master branch to Heroku to deploy it, and migrate your database
  - Check if your API is publicly available online!
3. Create a simple client interface application
  - Create controllers, services, and Slim views for:
    - a layout template with navigation bar (Home/login/register or Home/account/logout)
    - a home page
    - a login page
    - an account overview page for logged in users
  - Allow users to login using the login page
    - Use a service object call to authenticate the user with your API
    - Use a cookie to store the logged in user's username and other information
  - Allow users to logout by destroying their cookie and any objects with their information
  - Allow logged in users to see their account information
4. Create Github issues for what security weaknesses our interface / API face
5. IMPORTANT: do some research on how Rack cookies with a 'secret' are encoded
  - See the [Ruby documentation](http://www.rubydoc.info/github/rack/rack/Rack/Session/Cookie) to see how to specify a 'secret' to add security to encoded cookies
  - Do some research (maybe look at the source code for Rack) to see how the 'secret' is used to encode cookies.
  - Add a description of how secured cookies are encoded as a github issues.
  - Also add to the issue any thoughts on vulnerabilities of this method.
