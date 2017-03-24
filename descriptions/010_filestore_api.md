## A. Basic File Store API

This week your team will create the beginnings of an API to perform your service

1. Create a basic API based on the project we saw in class [(see the `0_filestore_api` branch of the in-class demo app)](https://github.com/ISS-Security/configshare/tree/0_filestore_api)
  - **Do NOT clone or fork from the class demo project!**
  - Create the appropriate resource class for your project in the `models/` folder
  - Create an appropriately named Sinatra-based API class in `app.rb`
  - Create the appropriate setup files (`Gemfile`, `config.ru`, `Procfile`)
  - Store resources for users in a `db/` folder

2. Create HTTP routes for your API that users can access
  - one GET route to return an index of all resources (e.g., GET `/api/v1/resources`, where 'resources' is the name of your particular resources: files/pictures/passwords, etc.)
  - one GET route to return details of a specific resource (e.g., GET `/api/v1/resources/[ID].json`) to return jsonified resource with ID (metadata + data)
  - OPTIONAL: one GET route to return a particular attribute of a resource (e.g., GET `/api/v1/resources/[ID]/attribute`, where 'attribute' is a particular attribute for your resource: document/photo/password, etc.)
  - OPTIONAL: one POST route to create a new resource, given json information about it (e.g., POST `/api/v1/resources`)

3. Identify security issues your application currently faces
  - Think about weaknesses in confidentiality, integrity, authentication, authorization, availability,
  - Create **Github Issues** for these vulnerabilities
    - create one issue for each vulnerability
    - detail what the vulnerability is (what is at risk)
    - explain how it can be exploited (what an attacker might do to execute an attack)
    - we will try to resolve these vulnerabilities in future weeks

We will demo some of the apps and discuss your Github issues in class!
