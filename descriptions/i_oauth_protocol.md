# I. Single Sign-On Using OAuth an Single Table Inheritance

This week we will implement single sign-on (SSO) to allow users to login using their Github credentials. But first, we must setup our database (API) to handle two types of accounts: regular accounts (Account) and SSO accounts (SSOaccount).

1. API: Single-Table Inheritance
  - Rename accounts table
    - rename your `accounts` migration and table to `base_accounts`
    - create a new column in `base_accounts` table of `String :type`
    - find all references to `:accounts` table in other migrations and also call them `:base_accounts`
  - Model Inheritance
    - `BaseAccount` model
      - move all the code from your `Account` model into a new model called `BaseAccount`
      - BaseAccount should inherit from `Sequel::Model`
    - `Account` model
      - move the methods `password` and `password=` back into your `Account` model
      - `Account` should inherit from `BaseAccount`
    - `SsoAccount` model
      - create a new, empty `SsoAccount` model
      - `SsoAccount` should inherit from `BaseAccount`
  - Services Refactoring
    - Identify service objects that use the `Account` model
      - note: you should not be calling any models in your controllers!
      - choose whether each service should use `BaseAccount`, `Account`, or `SsoAccount`
      - create a new service object and controller route to retrieve (or create) `SsoAccount` accounts
2. App & API: Distributed Single Sign-On
  - There are four steps to OAuth based SSO
    - (one time only) register your app with Github as an OAuth developer application
    - user clicks on link to Github with `CLIENT_ID`
    - Github authorizes app and redirects user back to a callback URL with a `code`
    - POST request to Github with `GH_CLIENT_ID`, `GH_SECRET`, `code` to get an `access_token`
    - GET request to Github with `access_token` to retrieve Github account information (login, email)
  - Choose from three options (see class handout) of how to distribute these tasks between your App and your API
    - option 1: App handles everything and asks API to find/create Github account
    - option 2: App and API share responsibilities
    - option 3: API handles everything and returns Github account to App
  - Make sure at the end that your API stores a new `SsoAccount` if one does not exist for an SSO login

3. OPTIONAL: hardened and granular authorization
  - Replace `username` from API routes with `id` of user
    - this makes it harder for anyone who has stolen a token to call API (they won't know the `id`)
    - effectively means that an attacker would have to know something (`id`) and have something (`auth_token`)
  - Add privileges to `auth_token`
    - Have a new field in token hash called `privileges`, with values such as `'read'`, `'read write'`, etc.
    - Check 'write' privileges if API route changes data (e.g., all POST resource routes)
    - This allows us to create tokens for read only access if needed
