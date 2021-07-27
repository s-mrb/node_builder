## About

This readme contains guide regarding the use of `nodebuilder`.

## What is `nodebuilder`

`nodebuilder` is a tool to convert wireframes into MVP using a simple schema that defines your wireframe.

## Usagae via example wireframe
We will refer to [this]() wireframe for this example.

- clone [node_builder]() repository
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
  companies:company_name,employees;
  content:invite_text,register_text,register_header;
  ```
- Once you are done with Models hit `Convert Model` button, you will be asked to select data types for each field, hit `Generate JSON` after you are done with selecting data types for each field, you will get a `configuration` text in box below `Generate JSON` button. 
- Copy the enire configuration text from the box that is directly underneath `Generate JSON` button.
- Paste copied configurations in `path2cloned_node_builder_repo/scripts/configurations.json` if there were any previous configurations inside `configurations.json` then just replace it.
