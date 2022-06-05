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
> .PHONY: objectname
```
.PHONY: main
all: main test
    gcc -o simple  main.o test.o 
main:
    gcc -o main.o -c main.c
test:
    gcc -o test.o -c test.c
clean:
    rm test.o main.o simple
```

## 变量

```
.PHONY: clean main
RM = rm
CC = gcc
OBJS = main.o foo.o
EXE = simple
${EXE}:${OBJS}
        ${CC} -o ${EXE} ${OBJS}
foo.o: foo.c
        ${CC} -o foo.o -c foo.c
main.o: main.c
        ${CC} -o main.o -c main.c
clean:
        ${RM} ${EXE} ${OBJS}

```

## 自动变量

```
.PHONY: clean main
RM = rm
CC = gcc
EXE = simple
SRCS = ${wildcard *.c}    <!-- wildcard 通配符自动填入.c文件 -->
OBJS = ${patsubst %.c, %.o, ${SRCS}} <!-- patsubst 将.c 替换为.o -->
${EXE}:${OBJS}
    ${CC} -o ${EXE}  &{OBJS}
main.o: main.c
    ${CC} -o main.o -c main.c
foo.o: foo.c
    ${CC} -o foo.o -c foo.c
clean:
    ${RM} ${EXE} ${OBJS}
```