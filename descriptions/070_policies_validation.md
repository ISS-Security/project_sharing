# Validated Form Input and Enforce SSL

This week we will create centralized resource policies, and validate user input coming from web forms. See the latest version of our demo project:
- [Web API: auth_policy](https://github.com/ISS-Security/configshare-api/tree/6_auth_policy)
- [Web App: authorized_access](https://github.com/ISS-Security/configshare-app/tree/4_policy_validation)

1. Formal Policies
  - API: Create policy objects in a `/policies` folder of your API
    - Create at least one policy object per resource (e.g., 'ProjectPolicy', 'ConfigFilePolicy', etc.)
    - Initialize policy objects with appropriate model objects (e.g., account seeking to access resource, particular resource)
    - Create true/false predicate methods check for key actions (creation/deletion/updating/viewing, etc.)
    - Make your predicate methods readable by using descriptive private helper methods
    - Use your policy objects in each API resource route to check authorization of agent
  - API: Create policy scope objects
    - Scope objects should return lists of all relevant objects for a given action (e.g., `viewable`) and agents (e.g., `current_account`)
    - Scope objects could evaluate permission of account requesting access
    - Use your policy scope objects to retrieve list of objects to return on index routes (e.g., `/api/v1/accounts/:id/projects`)
  - API + Web App: Policy summaries
    - API: Create a `summary` method for each policy object that returns a hash of all predicate names and results
    - API: Routes that return a resource should return a jsonified summary of its policy for the given account
    - Web App: Forms should determine authorization to show links/buttons/resources based on policy summaries returned by API
3. Web App: Validating Form input
  - Use the `dry-validation` gem to create validation schema for your views
    - Every view should have a unique schema defined by a *form object*
    - Put your form objects in a new `/forms` directory
    - Create custom rules for rules that use multiple input fields
    - Choose between using `dry-validation`'s messages and creating custom error messages
  - Use form objects in your controllers
    - Pass your `params` directly to your form objects
    - See that your controllers are now using only form objects and service objects to handle all non-routing logic
