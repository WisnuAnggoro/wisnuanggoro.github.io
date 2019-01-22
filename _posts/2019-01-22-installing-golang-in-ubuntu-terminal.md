---
layout: post
title: "Installing Golang in Ubuntu Terminal"
date: 2019-01-22
---
# Installing Go
* Update and upgrade the Ubuntu package by running the following two commands:
```bash
    sudo apt-get update
    sudo apt-get -y upgrade
```
* Get the url address to download stable package of Go by visit https://golang.org/dl/ then copy the link address.
* Download Go package by running the following command. Assume that the url address that is fetched from previous step is https://dl.google.com/go/go1.11.4.linux-amd64.tar.gz so command will be as follow:
```bash
    curl -O https://dl.google.com/go/go1.11.4.linux-amd64.tar.gz
```
* Unpack the package using the following command:
```bash
    tar -xvf go1.11.4.linux-amd64.tar.gz
```
* Move the unpacked Go package to _/usr/local_
```bash
    sudo mv go /usr/local
```
# Setting up GOPATH
* Open .profile file as follow:
```bash
    sudo nano ~/.profile
```
* Add the following lines at the end of file:
```bash
    export GOPATH=$HOME/goprojects
    export PATH=$PATH:/usr/local/go/bin:$GOPATH/bin
```
* Refresh the profile by running following command:
```bash
    source ~/.profile
```
* Create the workspace folder as follow:
```bash
    mkdir $HOME/goprojects
```
# Testing Go Installation
* Type the following command to find out the Go version. It should show the version of installed Go.
```bash
    go version
```
* Download HelloWorld code by running the following command:
```bash
    go get github.com/golang/example/hello
```
* Wait a moment until it download the code completely, then execute the following command:
```bash
    $GOPATH/bin/hello
```