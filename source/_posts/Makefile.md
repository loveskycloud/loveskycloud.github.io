---
title: Makefile
date: 2022-06-04 22:15:00
tags:
---

## 目标
> make 后面不跟目标默认执行第一个
> `@`为不显示该命令
```
all:
    @echo "hello world"

test: 
    @echo "hello test"
```
> make
```
    hello world
```

## 依赖

> 执行目标会先执行他的依赖
* 依赖执行顺序从左到右

```
all: test
    @echo "hello world"
test:
    @echo "hello test"
```
> make
```
hello test
hello world
```

## 伪对象
> .PYTHON: objectname
```
.PYTHON: main
all: main test
    gcc -o simple  main.o test.o 
main:
    gcc -o main.o -c main.c
test:
    gcc -o test.o -c test.c
clean:
    rm test.o main.o simple
```