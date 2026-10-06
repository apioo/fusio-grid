
<p align="center">
    <a href="https://www.fusio-project.org/" target="_blank"><img src="https://www.fusio-project.org/img/fusio_64px.png"></a>
</p>

# Fusio Grid

> Instant, production-ready REST APIs directly from your relational database grid.

Fusio Grid is a specialized distribution and toolset for Fusio designed to automatically expose relational databases as
secure, type-safe REST APIs. By performing automated schema reflection via Doctrine DBAL, Fusio Grid generates
TypeSchema definitions, CRUD actions, and explicit routes for every table in your database in seconds.

## Key Features

* __Instant REST Endpoints__: Provisions full CRUD endpoints (`GET`, `POST`, `PUT`, `DELETE`) for every table in your database under a clean base path (`/{connection_name}/{table_name}`).
* __Type-Safe Schemas__: Automatically inspects database columns, nullability, and foreign keys to build strict TypeSchema definitions.
* __OpenAPI & SDK Generation__: Generates comprehensive OpenAPI specifications and enables instant client SDK generation (TypeScript, Python, PHP, Java, Go, C#) via Fusio’s core capabilities.
* __Production-Ready Gateway Features__: Out-of-the-box support for API key authentication, OAuth2, rate limiting, and request validation.
* __Interactive & CI/CD Friendly__: Setup your API interactively via terminal prompts or run headlessly in CI/CD pipelines and Docker entrypoints using CLI options.
* __Seamless Fusio Upgrade Path__: If your requirements grow beyond automated CRUD operations, every generated route, action, and schema remains fully editable within the standard Fusio dashboard.

## Quick Start

### Interactive Setup

Run the `grid:setup` command to interactively configure a database connection and build the API:

```bash
php bin/fusio grid:setup
```

The interactive prompt guides you through:

* Naming your connection / path prefix (e.g., `shop`).
* Selecting your database driver (MySQL / MariaDB, PostgreSQL, or SQLite).
* Entering host, database name, user, and password credentials.
* Previewing the generated schemas, actions, and routes before provisioning.

### Non-Interactive / Headless Setup (CI/CD & Docker)

Pass connection parameters directly as CLI flags to execute in automated environments:

```bash
php bin/fusio grid:setup ecommerce \
  --driver=pdo_mysql \
  --host=127.0.0.1 \
  --port=3306 \
  --dbname=ecommerce_prod \
  --user=db_user \
  --password=secret_pass \
  --prefix=app_
```

If the connection name argument (`ecommerce`) is omitted, Fusio Grid automatically infers the path prefix from the
`--dbname` option.

## Generated Endpoint Architecture

For a database connection named `inventory` containing an `items` table, Fusio Grid provisions the following REST
endpoints under:
https://api.yourdomain.com/inventory/items


| HTTP Method | Route | Description | Request Body | Response Body |
| ------------|-------|-------------|--------------|-------------- |
| `GET`     | `/inventory/items` | List records with pagination, filtering & sorting | None | ItemCollection |
| `POST` | `/inventory/items` | Create a new record | `Item` | `Message`
| `GET` | `/inventory/items/:id` | Fetch a single record by primary key | None | `Item`
| `PUT` | `/inventory/items/:id` | Update an existing record | `Item` | `Message`
| `DELETE` | `/inventory/items/:id` | Delete a record by primary key | None | `Message`



This is a starter project for using [Fusio](https://github.com/apioo/fusio) as a framework. You can find general
information about Fusio on the [website](https://www.fusio-project.org/), in the [docs](https://docs.fusio-project.org/),
and in the GitHub [repository](https://github.com/apioo/fusio).

## CLI Command Reference

```bash
php bin/fusio grid:setup [name] [options]
```

### Arguments

* `name`(optional) - Name of the connection and base URL path segment (e.g., `shop`). Inferred from `--dbname` if not supplied.

### Options

* `-d`, `--driver` – Database driver (pdo_mysql, pdo_pgsql, pdo_sqlite). Default: pdo_mysql.
* `-H`, `--host` – Database host address. Default: 127.0.0.1.
* `-P`, `--port` – Database port number.
* `-D`, `--dbname` – Database name.
* `-u`, `--user` – Database user.
* `-p`, `--password` – Database password.
* `-t`, `--prefix` – Optional table prefix to filter reflected tables.

## Ecosystem

Fusio Grid is part of the Fusio open-source platform ecosystem:

* __Fusio__ – The central API management engine and reaction reactor.
* __Fusio Plant__ – Self-hosted server deployment and runtime hosting platform.
* __Fusio Grid__ – The automated database-to-REST distribution network.

