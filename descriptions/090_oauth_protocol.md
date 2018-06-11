# Single Sign-On Using OAuth

This week we will implement single sign-on (SSO) to allow users to login using their Github credentials. But first, we must setup our database (API) to handle three types of accounts: any account (Account), only email registered accounts (EmailAccount), and only SSO accounts (SSOaccount).

## 1. API: Single-Table Inheritance

- Let your `accounts` table handle types: add a new column to handle types (e.g., `type`)
- Model Inheritance
  - `Account` model
    - Move all the password related code from your earlier `Account` model into a new model called `EmailAccount`
    - Account should still inherit from `Sequel::Model`
  - `EmailAccount` model
    - Make your new `EmailAccount` model inherit from `Account`
    - only keep methods like `password` and `password=` that relate to email registered accounts
  - `SsoAccount` model
    - create a new, empty `SsoAccount` model -- it can collect SSO specific behaviors later if you'd like
    - `SsoAccount` should inherit from `Account`
- Service and Controller Refactoring
  - Identify service objects and controllers that use the old `Account` model
    - Choose whether to use use `Account`, `Account`, or `SsoAccount` based on its specific task

## 2. App & API: Distributed Single Sign-On

- There are four steps to OAuth based SSO
  - (one time only) register your app with Github as an OAuth developer application
  - user clicks on link to Github with `CLIENT_ID` and scope (e.g., request email address)
  - Github authorizes app and redirects browser back to a callback URL with a `code`
  - POST request to Github with `GH_CLIENT_ID`, `GH_SECRET`, `code` to get an `access_token`
  - GET request to Github with `access_token` to retrieve Github account information (login, email)
- Use the method we saw in class to split OAuth tasks between API and App
  - App intiates and completes SSO authorization processes up until it gets an `access_token`
  - App sends `access_token` to API
  - API uses `access_token` to retrieve user data from Github
  - API creates new `SsoAccount` and returns `account` and `auth_token` data to App
- Make sure at the end that your API stores a new `SsoAccount` if one does not exist for an SSO login
