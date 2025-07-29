static:
	ar rcs lib/static/libhello.a obj/helloLam.o obj/helloworld.o

link:
	gcc obj/main.o -Llib/static -lhello -o bin/exam

all:
	gcc -c main.c -o obj/main.o -I./inc
	gcc -c src/helloLam.c -o obj/helloLam.o -I./inc
	gcc -c src/helloworld.c -o obj/helloworld.o -I./inc

clean:
	rm -rf obj/* bin/*
