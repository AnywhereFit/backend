# Fitness Anywhere Back End

## Heroku git URL:

https://fitanywhere.herokuapp.com/

[POST] /api/auth/register ( Creates a user using the information sent inside the `request body` )
[POST] /api/auth/login
[GET] /api/users (TOKEN REQUIRED - RESTRICTED - only users with a valid token can access)
[GET] /api/user/:user_id (TOKEN REQUIRED - RESTRICTED)
[GET] /api/classes (TOKEN REQUIRED - RESTRICTED)
[GET] /api/classes/:class_id (TOKEN REQUIRED - RESTRICTED)
[PUT] /api/classes/:class_id | Updates the class with the specified `id` using data from the `request body`. Returns the modified class
[DELETE] /api/classes/:class_id | Removes the class with the specified `id` using data from the `request body`. Returns the deleted class
[GET] /api/classes/:user_id/attending (TOKEN REQUIRED - RESTRICTED)
[GET] /api/classes/:user_id/instructing (TOKEN REQUIRED - RESTRICTED)

Authentication will be implemented using JSON Web Tokens.

USER endpoints:

to register a new user account requires the following:

[POST] /api/auth/register

[1] username
[2] password
[3] role

to sign in/login into account requires the following:

[1] username
[2] password

How to use it on Postman:

https://fitanywhere.herokuapp.com/api/auth/register example : on postman => Select Body - chose raw and change where it said text to JSON

{
"username":"Priscila",
"role": "instructor",
"password":"1234"
}
a successful response will look like this :
{
"username": "Priscila"
}

to sign in to the created account use [POST] method to the following address
https://fitanywhere.herokuapp.com/api/auth/login
a successful response will send back a token and response will look like the following:

{
"message": "welcome Joe ",
"token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWJqZWN0IjoxLCJ1c2VybmFtZSI6Imhlcm9rdXRlc3QiLCJwYXNzd29yZCI6IiQyYSQwOCRFLjMwLzdUSjY3RmZUZmFhNTNUL2kudmJ0ZktsVnlESDhIY01ua2ZGMlRWeURES0wxeDRFSyIsImlhdCI6MTYzNzExNTUxNCwiZXhwIjoxNjM3MjAxOTE0fQ.2V8KVc5o6yTc-0cVkNRGwebdg4Nk6ejxbIUPGWMUQxg"
}

[GET] /api/users (TOKEN REQUIRED - RESTRICTED)

[
{
"user_id": 1,
"username": "Priscila",
"password": "hashedpassword",
"role_type": "instructor",
"created_at": "",
"updated_at": ""
},
{
"user_id": 2,
"username": "Andrew",
"password": "hashedpassword",
"role_type": "client",
"created_at": "",
"updated_at": ""
}
]

[GET] /api/user/:user_id (TOKEN REQUIRED - RESTRICTED)

{
"user_id": 1,
"username": "Priscila",
"password": "hashedpassword",
"role_type": "instructor",
"created_at": "",
"updated_at": ""
}

CLASSES ENDPOINTS:

[GET] /api/classes (TOKEN REQUIRED - RESTRICTED)

[
{
"class_id": 1,
"class_name": "Ashtanga Yoga",
"class_duration": "45 min",
"max_class_size": 10,
"class_date": "...",
"start_time": "10:00:00",
"class_location": "La Jolla",
"class_type": "Yoga",
"class_intensity": "Beginner",
"class_instructor": 1
},
{
"class_id": 2,
"class_name": "Swimming for beginners",
"class_duration": "1 hour",
"max_class_size": 12,
"class_date": "...",
"start_time": "12:30:00",
"class_location": "PIER 42 - Pacific Beach",
"class_type": "swimming",
"class_intensity": "Beginner",
"class_instructor": 2
},
{
"class_id": 3,
"class_name": "Hot Yoga",
"class_duration": "1 hour",
"max_class_size": 25,
"class_date": "...",
"start_time": "07:00:00",
"class_location": "Body Fit Gym",
"class_type": "Yoga",
"class_intensity": "Advanced",
"class_instructor": 1
}
]

[GET] /api/classes/:class_id (TOKEN REQUIRED - RESTRICTED)

Will return:

{
"class_id": 1,
"class_name": "Hot Yoga",
"class_duration": "1 hour",
"max_class_size": 25,
"class_date": "...",
"start_time": "07:00:00",
"class_location": "Body Fit Gym",
"class_type": "Yoga",
"class_intensity": "Advanced",
"class_instructor": 1
}

[GET] /api/classes/:user_id/attending (TOKEN REQUIRED - RESTRICTED)

A specific user can get all classes that will attend.

[
{
"user_id": 2,
"username": "Andrew",
"class_id": 1,
"class_name": "Hot Yoga",
"class_duration": "1 hour",
"max_class_size": 25,
"class_date": "...",
"start_time": "07:00:00",
"class_location": "Body Fit Gym",
"class_type": "Yoga",
"class_intensity": "Advanced",
"class_instructor": 1
},
{
"user_id": 2,
"username": "Andrew",
"class_id": 1,
"class_name": "Ashtanga Yoga",
"class_duration": "45 min",
"max_class_size": 10,
"class_date": "...",
"start_time": "10:00:00",
"class_location": "La Jolla",
"class_type": "Yoga",
"class_intensity": "Beginner",
"class_instructor": 1
}
]

[GET] /api/classes/:user_id/instructing (TOKEN REQUIRED - RESTRICTED)

A specific instructor can get all classes that will instruct.

[
{
"username": "Priscila"
"class_id": 1,
"class_name": "Ashtanga Yoga",
"class_duration": "45 min",
"max_class_size": 10,
"class_date": "...",
"start_time": "10:00:00",
"class_location": "La Jolla",
"class_type": "Yoga",
"class_intensity": "Beginner",
"class_instructor": 1
"number_registered": 10
},
{
"class_id": 3,
"class_name": "Hot Yoga",
"class_duration": "1 hour",
"max_class_size": 25,
"class_date": "...",
"start_time": "07:00:00",
"class_location": "Body Fit Gym",
"class_type": "Yoga",
"class_intensity": "Advanced",
"class_instructor": 1
"number_registered": 20
}
]

config Vars:

key
DATABASE_URL

Value
postgres://luhpcmpnmnrjbq:447620f131aea7135940123403c4e8c3e584d4e6397d53bcaff2182a09b3e146@ec2-52-70-205-234.compute-1.amazonaws.com:5432/d5a5jt3qfmj0ea

## Contributors

Thanks goes to these back end people:

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
<table>

<tr>
<td align="center"><a href="https://github.com/djho57"><img src="https://avatars.githubusercontent.com/u/88899732?v=4" width="90px;" alt="Daniel Ho"/><br /><sub><b>Daniel Ho</b></sub></a>
</tr>

<td align="center"><a href="https://github.com/PriscilaMonteiro "><img src="https://avatars.githubusercontent.com/u/77358128?v=4" width="90px;" alt="Priscila Monteiro"/><br /><sub><b>Priscila Monteiro</b></sub></a><br />

# Build Week Scaffolding for Node and PostgreSQL

## Video Tutorial

The following tutorial explains how to set up this project using PostgreSQL and Heroku.

[![Setting up PostgreSQL for Build Week](https://img.youtube.com/vi/kTO_tf4L23I/maxresdefault.jpg)](https://www.youtube.com/watch?v=kTO_tf4L23I)

## Requirements

- [PostgreSQL, pgAdmin 4](https://www.postgresql.org/download/) and [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) installed in your local machine.
- A Heroku app with the [Heroku PostgreSQL Addon](https://devcenter.heroku.com/articles/heroku-postgresql#provisioning-heroku-postgres) added to it.
- Development and testing databases created with [pgAdmin 4](https://www.pgadmin.org/docs/pgadmin4/4.29/database_dialog.html).

## Starting a New Project

- Create a new repository using this template, and clone it to your local.
- Create a `.env` file and follow the instructions inside `knexfile.js`.
- Fix the scripts inside `package.json` to use your Heroku app.

## Scripts

- **start**: Runs the app in production.
- **server**: Runs the app in development.
- **migrate**: Migrates the local development database to the latest.
- **rollback**: Rolls back migrations in the local development database.
- **seed**: Truncates all tables in the local development database, feel free to add more seed files.
- **test**: Runs tests.
- **deploy**: Deploys the main branch to Heroku.

**The following scripts NEED TO BE EDITED before using: replace `YOUR_HEROKU_APP_NAME`**

- **migrateh**: Migrates the Heroku database to the latest.
- **rollbackh**: Rolls back migrations in the Heroku database.
- **databaseh**: Interact with the Heroku database from the command line using psql.
- **seedh**: Runs all seeds in the Heroku database.

## Hot Tips

- Figure out the connection to the database and deployment before writing any code.

- If you need to make changes to a migration file that has already been released to Heroku, follow this sequence:

  1. Roll back migrations in the Heroku database
  2. Deploy the latest code to Heroku
  3. Migrate the Heroku database to the latest

- If your frontend devs are clear on the shape of the data they need, you can quickly build provisional endpoints that return mock data. They shouldn't have to wait for you to build the entire backend.

- Keep your endpoints super lean: the bulk of the code belongs inside models and other middlewares.

- Validating and sanitizing client data using a library is much less work than doing it manually.

- Revealing crash messages to clients is a security risk, but during development it's helpful if your frontend devs are able to tell you what crashed.

- PostgreSQL comes with [fantastic built-in functions](https://hashrocket.com/blog/posts/faster-json-generation-with-postgresql) for hammering rows into whatever JSON shape.

- If you want to edit a migration that has already been released but don't want to lose all the data, make a new migration instead. This is a more realistic flow for production apps: prod databases are never migrated down. We can migrate Heroku down freely only because there's no valuable data from customers in it. In this sense, Heroku is acting more like a staging environment than production.

- If your fronted devs are interested in running the API locally, help them set up PostgreSQL & pgAdmin in their machines, and teach them how to run migrations in their local. This empowers them to (1) help you troubleshoot bugs, (2) obtain the latest code by simply doing `git pull` and (3) work with their own data, without it being wiped every time you roll back the Heroku db. Collaboration is more fun and direct, and you don't need to deploy as often.
