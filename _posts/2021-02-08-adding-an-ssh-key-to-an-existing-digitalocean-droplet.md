---
layout: post
title: "Adding an SSH key to an existing DigitalOcean droplet"
date: 2021-02-08
tags: [digitalocean, droplet, ssh, ssh-key, ssh-keygen, bashupload]
---

I've setup my DigitalOcean (DO) droplet so it cannot be accessed using password. However, when I replaced my local machine, I can no longer access my droplet since I've lost the private SSH Key. Fortunately, I can still access the remote server from Web Console, but it's too slow and laggy.

Here's what I do to add my current ssh key to the droplet:

## 1. Generate new ssh key pair in the current local machine

If there's no ssh key pair in the local machine (`$HOME/.ssh/`), generate a new one using the following command:
```bash
ssh-keygen -t rsa
```

Or, you can attached your email to the key using this command:
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

## 2. Save public key to another file

Use the following command to copy `id_rsa.pub` to `key.txt`:
```bash
cd ~
cat ~/.ssh/id_rsa.pub > key.txt
```

## 3. Upload the public key to a file sharing service

Run the following command:
```bash
curl https://bashupload.com/key.txt --data-binary @key.txt
```

The response will be a link to download the key. Save it to be utilize in the next step.

## 4. Login to DO droplet using Web Console then run these following command:
```bash
cd ~/.ssh
wget <link-from-previous-step->
cat key.txt >> authorized_keys
```

Note: ensure to use `>>` when running `cat` command so the key is appended (and not overwrite) the `authorized_keys` file

## 5. Access droplet from the new local machine

Run the following command to login to droplet through SSH:
```bash
ssh <username>@<ip-address>
```

---

Source links:<br />
[How to add an SSH key to an existing DigitalOcean droplet](https://dev.to/saunved/how-to-add-an-ssh-key-to-an-existing-digitalocean-droplet-2mob)<br />
[Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)