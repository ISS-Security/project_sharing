# Secure Sessions

This week we will secure the storage of session state across our system and on the client machine. See the latest version of our demo code.

1. Deploy your API and App to Heroku
- API: setup and integrate PostGres database
- APP: Ensure that it is talking to the deployed API

2. Enforce SSL connections for Web App
- Use the `rack-ssl-enforcer` gem to enforce SSL connections on *production* servers (will break development/testing)
- Redirect users to secure HTTPS connections
  - _warning_ adding an HSTS header to a server's response will tell browsers to never try HTTP again

3. Let's switch our session storage to server-side pool
- Provision a Redis machine on Heroku
- Specify Redis as our application's session store
- If you must store data in cookies for any non-session purposes, make sure to implement a strong session secret nonce

4. Encrypt session data
- Create a _secure messaging_ library for all outgoing messages
  - Create a class in `/lib` that can `encrypt` and `decrypt` any message
  - Use a secret key stored in environment variable `MSG_KEY`
  - Use the NaCl library (`rbnacl/libsodium`) for all cryptography
- Update _secure session_ library to provide encryption for session data
  - Create a class in `/lib` that can securely `set` and `get` session variables
  - Use the secure messaging library for all crypto – your secure session library should contain no crypto code

5. APP + API: Create a very basic (and risky) registration workflow
  - APP: Allow users to register accounts
    - Accept posts from a registration form with email, username, and password
    - Use a service object to post the data to your API
  - API: Create users given their email, username, and password
  - _Notice_: We have not performed any verification of account details
