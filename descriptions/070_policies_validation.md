# Policies and Validation

This week we will create centralized resource policies, and validate user input coming from web forms. See the latest version of our demo project:

## 1. Web App: Start creating "models" in your web application

- The `models/` folder can hold objects that convert incoming API data (arrays/hashes) back into native objects
- The demo app in class creates models for `Project`, `Projects`, `Document`, `User`, and `Session`

## 2. Web App: Validating Form input

- Use the `dry-validation` gem to create validation schema for your views
  - Every view should have a unique schema defined by a *form object* in a new `/forms` directory
  - Create custom rules if you need to compare two or more input fields
  - Choose between using `dry-validation`'s messages and creating custom error messages
- Use form objects in your controllers
  - Pass your `params` directly to your form objects
  - Check if form validation is a `success?`
  - Pass form object (not params) to service object if needed

## 3. Formal Policies

- API: Create policy objects in a `/policies`
  - Create at least one policy object per resource (e.g., 'ProjectPolicy', 'DocumentPolicy', etc.)
  - Initialize policy objects with appropriate models (subject and object of policy)
  - Create true/false predicate methods check for key actions (creation/deletion/updating/viewing, etc.)
  - Make your predicate methods readable by using descriptive private predictes
  - Use your policy objects in resource request routes to check authorization of account and resource
- API: Create policy scope objects
  - Scope objects should return lists of all relevant objects for a given action (e.g., `viewable`) and agents (e.g., `current_account`)
  - Use your policy scopes to retrieve lists of objects to return on index routes (e.g., `/api/v1/projects`)
- API + Web App: Policy summaries
  - API: Create a `summary` method for each policy object that returns a hash of all predicate names and results
  - API: Routes that return a resource should return a jsonified summary of its policy for the given account
  - Web App: Forms should determine authorization to show links/buttons/resources based on policy summaries returned by API
