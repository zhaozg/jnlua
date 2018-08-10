# Paths
JDK_DIR=${JAVA_HOME}
LUA_LIB_DIR=${HOME}/work/lua-forge/luajit/src
LUA_INC_DIR=${HOME}/work/lua-forge/luajit/src
VERSION=5.1

# Tools
CC=gcc
LD=gcc

# Default arguments
CFLAGS=-c -fno-strict-aliasing -m64 -fPIC -O2 -Wall -DNDEBUG -D_REENTRANT -DLUA_USE_POSIX
LDFLAGS=-m64 -bundle -undefined dynamic_lookup -lm

# Description blocks
all: libjnlua$(VERSION).dylib javavm.so

libjnlua$(VERSION).dylib: jnlua.o
	$(LD) $(LDFLAGS) -o libjnlua$(VERSION).dylib jnlua.o

jnlua.o: ../jnlua.c
	$(CC) $(CFLAGS) -I$(JDK_DIR)/include -I${JDK_DIR}/include/darwin -I$(LUA_INC_DIR) ../jnlua.c

javavm.so: javavm.o
	$(LD) $(LDFLAGS) -o javavm.so javavm.o -L$(JDK_DIR)/lib/server -ljvm

javavm.o: ../javavm.c ../javavm.h
	$(CC) $(CFLAGS) -I$(JDK_DIR)/include -I$(JDK_DIR)/include/darwin -I$(LUA_INC_DIR) ../javavm.c

clean:
	-rm *.o *.so *.dylib
