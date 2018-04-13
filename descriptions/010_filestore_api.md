## Basic File Store API

This week your team will create the beginnings of an API to perform your service. For this week's coding, you can refer to the `0_api_filestore` branch of the demo project we are seeing in class.

### Notes
- Make sure all your classes belong to a module that bears the name of your project (e.g., `Credence` or `Wallet`, etc.)
- Make sure you create a Github repo for your team that all members can work on (store the repo under your team's organization and try to ensure that your teammates all contribute in some way).

### 1. Create a basic domain resource entity class (demo example: `Credence::Document`)
- Choose the most important resource or entity related to your project idea
  - e.g., File, Image, URL, etc.
  - Do NOT pick 'User' for now (we will discuss users in class later)
- Create the appropriate resource class for your project in the `models/` folder
  - The `initialize` method should create a new object of this resource
  - Create a `#new_id` for new objects
  - Make sure your model has instance methods to `#save` a new entity and to convert the entire resource `#to_json`
  - Make sure your model has class methods to `::find` an existing entity and find `::all` entitites
  - Store and retrieve resources as json text files in a `db/` folder
  - You might have to encode some attributes (e.g., large text) as Base64

### 2. Create a Web API
- Create an appropriately named Roda-based API class in `app.rb`
- Create the appropriate setup files (`Gemfile`, `config.ru`) we discussed in class
- `.gitignore` files in `db/*.*` (this means files with extensions in the `db/` folder, but not in subfolders)
- Create a root route (`/`) that returns a basic json message (outside resources often check this route to see if your service is alive)
- Create one POST route to create a new resource, given json information about it (e.g., `POST /api/v1/[resources]`), where '[resources]' is the name of your particular resources: files/pictures, etc.)
- create one GET route to return details of a specific resource (e.g., `GET /api/v1/[resources]/[ID].json`) to return jsonified resource with ID (metadata + data)
- create one GET route to return an index of all resources (e.g., `GET /api/v1/[resources]` would return IDs of all resources as json)
- Create a helpful `README.md` with instructions on how to use your API, including all routes (keep this README up-to-date throughout the project)
- Create a `LICENSE` file with terms of how your code can be adapted by others (see [choosealicense.com](https://choosealicense.com) for help on picking a license)

### 3. Identify security issues your application currently faces
- Think about weaknesses in confidentiality, integrity, authentication, authorization, availability, non-repudiation
  - in particular, think how a hacker might try to infiltrate the Web API you have created so far
- Create **Github Issues** for these vulnerabilities
  - create one issue for each vulnerability
  - detail what the vulnerability is (what is at risk)
  - explain how it can be exploited (what an attacker might do to execute an attack)
  - we will try to resolve these vulnerabilities in future weeks

We will demo some of the apps and discuss your Github issues in class!
