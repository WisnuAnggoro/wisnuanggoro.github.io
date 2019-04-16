---
layout: post
title: "Setting Up a New Database on CockroachDB"
date: 2019-04-16
tags: [cockroachdb, database, sql, postgres, query]
---

These are what I usually do when setting up a new database in `CockroachDB` cluster:

## Show databases
```sql
SHOW DATABASES;
```

## Create table

The following sommand will create a new database named `new_db`:

```sql
CREATE DATABASE new_db;
```

## Grant privileges

By default, a new database is granteed to `root` and `admin` users. To grant others user to the database we can use `GRANT` command. The following query will grant `user1` to `new_db` database for `all`  privilege type:

```sql
GRANT ALL ON DATABASE new_db TO user1;
```

## Show grant

The following query will show all grantee to the selected database:

```sql
SHOW GRANTS ON DATABASE new_db;
```


---

Source links:<br />
[CREATE DATABASE](https://www.cockroachlabs.com/docs/stable/create-database.html)<br />
[GRANT `<privileges>`](https://www.cockroachlabs.com/docs/stable/grant.html)