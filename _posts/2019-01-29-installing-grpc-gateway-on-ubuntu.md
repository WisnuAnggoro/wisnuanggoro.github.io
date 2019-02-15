---
layout: post
title: "Installing gRCP Gateway on Ubuntu"
date: 2019-01-29
tags: [golang, ubuntu, grpc]
---

## Preface

The installation procedure has been explained in its official repo [here](https://github.com/grpc-ecosystem/grpc-gateway). However, there are several tools we need to install before installing the gRCP Gateway plugin.

## Installing prerequisite tools

Run the following commands:
```bash
sudo apt update
sudo apt install build-essential libtool autoconf automake
```

## Installing ProtocolBuffers

Run the following commands to install `ProtocolBuffers`:
```bash
mkdir tmp
cd tmp
git clone https://github.com/protocolbuffers/protobuf
cd protobuf
./autogen.sh
./configure
make
make check
sudo make install
```

## Installing packages

Run the following commands to clone the repos to $GOPATH\src then install them:
```bash
go get -u github.com/grpc-ecosystem/grpc-gateway/protoc-gen-grpc-gateway
go get -u github.com/grpc-ecosystem/grpc-gateway/protoc-gen-swagger
go get -u github.com/golang/protobuf/protoc-gen-go
```

## Update LD_LIBRARY_PATH
After installing gRPC Gateway, Proto Compiler (protoc) may not be able to find shared libraries. Run one of the following commands:

```bash
sudo ldconfig
```

or

```bash
export LD_LIBRARY_PATH=/usr/local/lib
```

---

Source links:<br />
[gRCP Gateway installation guide](https://github.com/grpc-ecosystem/grpc-gateway#installation)<br />
[Solution of undefined macro](https://github.com/jmervine/httperf/issues/1)<br />
[Protobuf cannot find shared libraries](https://stackoverflow.com/a/25518702)
