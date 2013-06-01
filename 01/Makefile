# Makefile for Linux
CC=g++
LIBS=
CFLAGS=-Wall -O2 -g
LDFLAGS=

EXEC=tree_test
OBJS=src/main.cxx src/tree.cxx

ZIP=zip
ZIPFILE=übung1_lab.zip

$(EXEC): $(OBJS)
	$(CC) -o $(EXEC) $(CFLAGS) $(OBJS) $(LDFLAGS)

clean:
	rm -f *.o $(EXEC) $(ZIPFILE)

zip:
	$(ZIP) $(ZIPFILE) $$(git ls-tree -r HEAD | cut -f 2)
