---
layout: post
title: "Adding a New Database on MySQL Server"
date: 2021-02-07
tags: [mysql, database, sql, mysql-console, terminal]
---

I have a MySQL server on my remote server and need to create a new database for my Wordpress site.

Here's the step-by-step to create MySQL using MySQL Console:

## 1. Connect to the MySQL console

Run the following command to login to MySQL Console using the `root` account:
```bash
sudo mysql
```

## 2. Create a new Database
Run the following command to create a new database named `example_database`:
```mysql
CREATE DATABASE example_database;
```

## 3. Create new user (Optional)
If there's no any user or we need to assign a new user to the new database, run the following command:
```mysql
CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
```

By using preceeding command, we create a new user with username: `example_user` and password: `password`

**Note:** Do not forget to replace `password` with a secure password

## 4. Grant the new user to the new database
Run the following command to give `example_user` user permission over the `example_database` database:
```mysql
GRANT ALL ON example_database.* TO 'example_user'@'%';
```

## 5. Quit the MySQL Console
Run `exit` command in the MySQL Console to exit the shell.

---

Source links:<br />
[How To Install Linux, Apache, MySQL, PHP (LAMP) stack on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-20-04#step-6-%E2%80%94-testing-database-connection-from-php-(optional))
