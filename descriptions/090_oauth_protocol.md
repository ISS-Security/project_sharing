# Single Sign-On Using OAuth an Single Table Inheritance

This week we will implement single sign-on (SSO) to allow users to login using their Github credentials. But first, we must setup our database (API) to handle two types of accounts: regular accounts (Account) and SSO accounts (SSOaccount).

1. API: Single-Table Inheritance
  - Rename accounts table
    - rename your `accounts` migration and table to `base_accounts`
    - create a new column in `base_accounts` table of `String :type`
    - find all references to `:accounts` table in other migrations and also call them `:base_accounts`
  - Model Inheritance
    - `BaseAccount` model
      - Move all the code from your earlier `Account` model into a new model called `BaseAccount`
      - BaseAccount should inherit from `Sequel::Model`
    - `Account` model
      - Make your earlier `Account` model inherit from `BaseAccount`
      - only keep the methods like `password` and `password=` that relate to registered accounts from your original `Account` model
    - `SsoAccount` model
      - create a new, empty `SsoAccount` model
      - `SsoAccount` should inherit from `BaseAccount`
  - Service and Controller Refactoring
    - Identify service objects and controllers that use the old `Account` model
      - choose whether to use use `BaseAccount`, `Account`, or `SsoAccount`
      - create a new service object and controller route to authenticate (and create) `SsoAccount` accounts
2. App & API: Distributed Single Sign-On
  - There are four steps to OAuth based SSO
    - (one time only) register your app with Github as an OAuth developer application
    - user clicks on link to Github with `CLIENT_ID`
    - Github authorizes app and redirects browser back to a callback URL with a `code`
    - POST request to Github with `GH_CLIENT_ID`, `GH_SECRET`, `code` to get an `access_token`
    - GET request to Github with `access_token` to retrieve Github account information (login, email)
  - Choose from the options we saw in class of how to distribute these tasks between your App and your API
    - ~~option 1: App handles everything and asks API to find/create Github account~~
    - option 2: App completes authorization and sends access_token to API, API uses access_token to retrieve user data from Github
    - option 3: API handles everything and returns Github account to App
  - Make sure at the end that your API stores a new `SsoAccount` if one does not exist for an SSO login
