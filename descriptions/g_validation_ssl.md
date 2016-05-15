# G. Validated Form Input and Enforce SSL

This week we are validating user input coming from web forms, and enforcing
SSL connections between essential parts of our architecture. Take a look at the
latest code for the app client at:
  - [Interface Client](https://github.com/ISS-Security/configshare-app/tree/3-validation_ssl)

1. Validating Form input
  - Use the `dry-validation` gem to create validation schema for your views
    - Every view should have a unique schema defined by a *form object*
    - Put your form objects in a new `/forms` directory
    - Create custom rules for rules that use multiple input fields
    - Choose between using `dry-validation`'s messages and creating custom error
      messages
  - Use form objects in your controllers
    - Pass your `params` directly to your form objects
    - See that your controllers are now using only form objects and service
      objects to handle all non-routing logic
2. Add flash messages for errors and notices
  - Use the `rack-flash3` gem to create flash messages
  - Add a flash message bar to your `layout.slim`
  - Create CSS file in `/public` folder for `:error` and `:notice` styles
    - Set the location of your public directory for Sinatra
  - Provide flash notices for form errors and important transitions (e.g., logout)
3. Enforce SSL connections
  - Use the `rack-ssl-enforcer` gem to enforce SSL connections on *production* servers (won't work during development/testing)
  - Enforce SSL for both your API and your web application
