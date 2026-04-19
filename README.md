# Cloudflare Pages Demo Collection

This repository contains a small set of Cloudflare Pages demos, from basic concepts to a blog-style practical example.

It focuses on these common Cloudflare Pages capabilities:

- text variables
- secrets
- KV bindings
- D1 bindings
- Pages Functions

## Repository Structure

- `env-demo/`
  - demonstrates text variables and secrets
  - useful for learning how `context.env.xxx` reads normal config values and sensitive values

- `bindings-demo/`
  - demonstrates a KV binding
  - uses a simple counter to show that a binding is not just a string, but a real resource object

- `d1-comments-demo/`
  - demonstrates a D1 database binding
  - uses comment creation and comment listing to explain how a database binding works

- `blog-practical-demo/`
  - combines text variables, secrets, KV, and D1 in one example
  - closer to a real blog-style Pages project

## Recommended Order

1. `env-demo`
2. `bindings-demo`
3. `d1-comments-demo`
4. `blog-practical-demo`

That order makes the learning path smoother:

- first understand variables and secrets
- then understand bindings
- then understand database bindings
- finally see how everything fits together in one blog example

## Demo Overview

### 1. env-demo

Directory: [`env-demo`](./env-demo)

This demo includes:

- `SITE_NAME` as a text variable
- `MY_TOKEN` as a secret

It shows:

- how a page calls `/api/site` to read a text variable
- how a page calls `/api/check` to validate a secret-backed token

### 2. bindings-demo

Directory: [`bindings-demo`](./bindings-demo)

This demo uses:

- `COUNTER` as a KV binding

It shows:

- `/api/counter` reading the current value
- `/api/increment` updating and incrementing the counter

This is useful for understanding that:

- a binding is not a plain string
- `context.env.COUNTER` is a real KV resource object
- you can call `.get()` and `.put()` on it directly

### 3. d1-comments-demo

Directory: [`d1-comments-demo`](./d1-comments-demo)

This demo uses:

- `DB` as a D1 binding

It shows:

- `/api/comment` inserting a comment
- `/api/comments` loading a comment list

This is useful for understanding:

- how to attach D1 to a Pages project
- the basic pattern of `context.env.DB.prepare(...).bind(...).run()`
- why structured data such as comments or metadata belongs in a database

### 4. blog-practical-demo

Directory: [`blog-practical-demo`](./blog-practical-demo)

This demo combines:

- text variables
  - `SITE_NAME`
  - `SITE_DESCRIPTION`
  - `ADMIN_EMAIL`
- secrets
  - `ADMIN_TOKEN`
- KV binding
  - `VIEWS`
- D1 binding
  - `DB`

It shows:

- loading site config from text variables
- updating article view counts with KV
- reading and writing comments with D1
- protecting an admin-style endpoint with a secret

## Deployment

Recommended approach:

1. connect this repository to Cloudflare Pages
2. choose one demo directory as the project root
3. configure the required variables, secrets, and bindings
4. redeploy

If you want one Pages project per demo, use these root directory values:

- `env-demo`
- `bindings-demo`
- `d1-comments-demo`
- `blog-practical-demo`

## Suggested Pages Build Settings

All demos use a very simple static-files-plus-`functions/` structure.

Typical settings:

- Framework preset: `None`
- Build command: leave empty
- Build output directory: `/`
- Root directory: set it to the selected demo folder

## Notes

- each demo folder has its own `README.md`
- specific variable names, binding names, and SQL setup steps are documented inside each demo folder
- if you only want to get one example working first, start with `env-demo`

## What You Will Learn

By working through these demos, you will understand:

- the difference between static assets and Pages Functions
- the difference between text variables and secrets
- the basic usage of KV and D1 bindings
- how to combine these features into a simple blog-style Pages project
