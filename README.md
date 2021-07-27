## About

This readme contains guide regarding the use of `nodebuilder`.

## What is `nodebuilder`

`nodebuilder` is a tool to convert wireframes into MVP using a simple schema that defines your wireframe.

## Usage via example wireframe
Clone [node_builder](http://104.225.217.239:3000/manaknight/paxifist) repository.
We will refer to [this](./wireframe.pdf) wireframe for this example.

### Generating `configurations.json`

- Go to wireframe [schema generator](https://webhook.manaknightdigital.com/schema/pre)
- From the top right radio buttons select node
- In `Portals` input write comma separated portals you want to create for your app.
  - Portals defines the segregation of users w.r.t their access privileges for your app.
  - Commonly you will just write `admin,members`, this means you want to establish two levels of privileges in your app aka `admin` and `members`. We will explore later the difference between levels of privileges.
- In the `Models` box you will write name of the `table` and their associated `fields`, a model is just a table in database.
  - It is assumed that there is 1-1 correspondence between tables in database of this app and the views of this app i.e in the database for this app (above given wireframe) there must be a `companies` table corresponding to the view on **page 3** and same is true for `content` and rest of the views.
  - You won't create `users` and `profile` view in `Models` box, they will be automatically created.
  - if you want to tell the nodebuilder to create `companies` table and `content` table, use below code in `Models` box,note that you won't use `id` and `action` fields while defining Model in `Models` box

  ```
  companies:company_name, employees;
  content:invite_text,register_text,register_header;
  company_users:company_name,employee,registered;
  questions:question_name,question_type,order,record_field_name,status;
  ```

- Once you are done with Models hit `Convert Model` button, you will be asked to select data types for each field, hit `Generate JSON`, remeber that data type for each fields that ends with "text" should be "text".
- After you are done with selecting data types for each field, you will get a `configuration` text in box below `Generate JSON` button. 
- Copy the enire configuration text from the box that is directly underneath `Generate JSON` button.
- Paste copied configurations in `path2cloned_node_builder_repo/scripts/configurations.json` if there were any previous configurations inside `configurations.json` then just replace it.

### Adding menus
Open `configurations.json` and search `menu` object, you will see something like this:

```js
   "menu": {
    "Dashboard": "/dashboard",
    "Users": "/users/0",
    "Profile": "/profile",
    "Logout": "/logout"
   }
```
It contains name to be displayed inside menu of app and the route to use when the view is clicked.
Menu object included the `views` to be placed inside `menu` of app.Dashboard, Users, Profile and Logout are automatically added in menu that's why we did not defined them inside `Models` in schema-generator.
Now to add Companies, Content and Questions view inside menu update the menu object as follows:

```js
   "menu": {
     "Dashboard": "/dashboard",
     "Users": "/users/0",
     "Companies": "/company/0",
     "Content": "/content",
     "Questions": "/questions",
     "Profile": "/profile",
     "Logout": "/logout"
   }
```

> Note: Route for views that have enabled pagination must start with first page i.e `/viewName/0`

### Installation
Before installation create a MySQL database (use any name) in your machine search `database` inside `configurations.js` then inside database update `username`, `password` and `database` with your MySQL username, password and database name. Also make sure that port inside `configutions.json` is also the one you are using for your MySQL server.

Run following commands inside `path2cloned_node_builder_repo/scripts/`, run them one by one:
```console
./initialize.sh
./localBuild.sh
./generate.sh
```
Last command will generate  code inside `release` folder.

Run the following command inside `path2cloned_node_builder_repo/release/`:
```console
npm i
```

Uncomment db code in `server.js` if it is commneted and run inside `release`:

```console
node server.js
```
Above step is needed if you don't already created databse in MySQL server.

To seed the database with the sample data, run this inside `release` folder:

```console
node seed.js
```

Now you are all set with first time setup.
Now whenever you need to run the code after making changes you have to run two commands:

```console
<!-- inside scripts folder -->
./initialize.sh

<!-- inside release folder -->
node server.js
```

## 

# Need to know

1. What actually is node_builder?
1. How to know which routes to enter using pagination syntax in menu object inside configurations.json?
1. Give the list of all field names that must not be supplied in Models box, e.g. index, and actions
1. Is there always 1-1 correspondence between views and table? 
    Got answer
1. Information regarding Default routes? 