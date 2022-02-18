# Morpheus


Morpheus is database migration tool for Neo4j written in Typescript.
> Morpheus is a modern, open-source, database migration tool for [Neo4j](http://neo4j.com).
> It is designed to be a simple, intuitive tool for database migrations.
> It is inspired by [Michael Simons tool for Java](https://github.com/michael-simons/neo4j-migrations).

## _*This project has been tested with `Neo4j 4.4.4`*_

# Installation

Install the latest version of Morpheus: 

```sh
npm install morpheus4j
```

Add a script to your project's package.json file:

  ```json
  "scripts": {
    "morpheus": "morpheus"
  }
  ```   

# Usage
### Create Migrations

You can create migrations by running the following command:

```sh
npm run morpheus create <migration_name>
```

Migrations will be created under the `neo4j/migrations` directory. Each migration will be a Cypher file with the name `<timestamp>_<migration_name>.cypher`.


### Initial Configuration

To run migrations, you need to configure Morpheus. To do so, create a `.morpheus.json` file in your project root directory and create a `neo4j/migrations` directory as well.

Or, you can use the `init` command:

```sh
npm run morpheus init
```

If you don't want to use a morpheus.json file, you can also use ENV variables as follows:

```env
NEO4J_SCHEME=neo4j
NEO4J_HOST=localhost
NEO4J_PORT=7687
NEO4J_USERNAME=neo4j
NEO4J_PASSWORD=neo4j
```

### Run Migrations

You can run migrations by running the following command:

```sh
npm run morpheus migrate
```
This will run all migrations in the `neo4j/migrations` directory.


# How it works
The approach is simple. Morpheus will read all migrations in the `neo4j/migrations` directory and execute them in order.

For each migration, Morpheus will create a transaction and execute the migration. Thus a migration may contain multiple Cypher statements (**each statement must end with `;`**).

Once a migration is executed, Morpheus will keep track of the migration and will not execute it again. 

Existing migration files that have already been executed **can not** be modified since they are stored in a database with their corresponding checksum.

If you want to revert a migration, create a new migration and revert the changes.