.PHONY: hello hellomake

CC := gcc
CFLASS := -I .

INC_FILES := hello.h

%.o: %.c $(INT_FILES)
	$(CC) -I. -c -o $@ $<

#main.o: main.c hello.h
#	$(CC) -I -c -o main.o main.c

test: hello.c hello.h
	@echo $@
	@echo $<
	@echo $^

hellomake: main.o hello.o
	$(CC) -o $@ main.o hello.o $(CFLASS)

hello: 
	gcc -o hello main.c hello.c -I.

clean:
	rm -rf hello hellomake *.o
