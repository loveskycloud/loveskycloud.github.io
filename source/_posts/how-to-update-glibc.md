---
title: How to update glibc
date: 2023-12-07 23:08:05
tags: glibc
---

> add under code in sources.list
```
deb http://security.debian.org/debian-security buster/updates main
```

> and 
```
sudo apt update
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 112695A0E562B32A 54404762BBB6E853
sudo apt install libc6-dev /sudo apt install libc6
```
* OK you get it
