---
layout: post
title: "Installing Redis in Ubuntu WSL (Windows Subsystem for Linux)"
date: 2019-03-08
tags: [wsl, ubuntu, windows, linux]
---

I found an straight-forward article about installing `Redis` in `Ubuntu 18.14` from [here](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-redis-on-ubuntu-18-04). I used the step-by-step article to install `Redis` in my `WSL` machine. However, there're several commands that cannot be run. Here's the complete step-by-step tutorial to install `Redis` on `Ubuntu WSL`:

## Update and upgrade `Ubuntu`

Run the following command to update and upgrade `Ubuntu`:

```bash
sudo apt update && apt upgrade
```

## Install `Redis`

Run the following command to install `Redis` on `Ubuntu`:

```bash
sudo apt install redis-server
```

## Update `redis.conf` file

Run the folowing command to open `redis.conf` file:

```bash
sudo nano /etc/redis/redis.conf
```

Find `supervised no` line and change to `supervised systemd` since `Ubuntu` uses the `systemd` init system.

## Start `Redis`

Run the following command to start `Redis`:

```bash
sudo service redis-server start
```

## Test `Redis`

Run the following command to run `redis-cli`:

```bash
redis-cli
```

Try to type `ping` in the `cli` to get a text `PONG`.

Run the following command to create a key named `test` containing `It's test`:

```bash
set test "It's test"
```

To get the value of the specified key, run the following command. Here we are going to fetch value of `test` key:

```bash
get test
```

Type `exit` to quit from `redis-cli`.

## Test `Redis` Persistant Data

Now, restart `Redis` by running the following command:

```bash
sudo service redis-server restart
```

Run `redis-cli` again then run `get test`. We should be displayed the value of `test` key which is `It's test`.

---

Source link<br />
[How To Install and Secure Redis on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-redis-on-ubuntu-18-04)<br />
[System has not been booted with systemd as init system (PID 1). Can't operate](https://stackoverflow.com/questions/52197246/system-has-not-been-booted-with-systemd-as-init-system-pid-1-cant-operate)<br />
[redis-cli cannot connect to redis-server.](https://github.com/Microsoft/WSL/issues/365)<br />
[How to configure Redis-Server on Bash on Ubuntu on Windows 10 (WSL)](https://blogs.technet.microsoft.com/jessicadeen/uncategorized/how-to-configure-redis-server-on-bash-on-ubuntu-on-windows-10-wsl/)