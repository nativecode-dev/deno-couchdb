# deno-couchdb

CouchDB client for Deno built top of fetch

# Usage

```ts
import { CouchClient } from "https://denopkg.com/keroxp/couch.ts";

export type User = {
  id: number;
  name: string;
  years: number[];
};
async function main() {
  // create couch client with endpoint
  const couch = new CouchClient("http://localhost:5984");
  // choose db to use
  const db = couch.database<User>("users");
  // check if specified database exists
  if (!(await couch.databaseExists("users"))) {
    // create new database
    await couch.createDatabase("users");
  }
  // insert new document
  const uesr = {
    id: 100,
    name: "deno",
    years: [2018, 2019]
  };
  const { id, rev } = await db.insert(user);
  // get existing document
  let user = await db.get(id); // {id: 100, name: "deno", years: [2018,2019]}
  // update existing document
  user.name.years.push(2020);
  await db.put(id, user, { rev });
  // delete existing document
  await db.delete(id);
}
```
# Compatibility Table

## Document

- [x] `HEAD /{db}/{docid}`
- [x] `GET /{db}/{docid}`
- [x] `PUT /{db}/{docid}`
- [x] `DELETE /{db}/{docid}`
- [x] `COPY /{db}/{docid}`

## Attachments

- [x] `HEAD /{db}/{docid}/{attname}`
- [x] `GET /{db}/{docid}/{attname}`
- [x] `PUT /{db}/{docid}/{attname}`
- [x] `DELETE /{db}/{docid}/{attname}`

## Server

- WIP...