UNAME := $(shell uname)
DEBUG=-g

CFLAGS=-c -Wall -O2 -funsigned-char  -Wno-write-strings -Wno-char-subscripts -Wno-strict-aliasing
CC=g++

ifeq ($(UNAME), Linux)
LDFLAGS= -lrt $(PGLOAD) 
endif

ifeq ($(UNAME), Darwin)
LDFLAGS=-mmacosx-version-min=10.7 $(PGLOAD)  
CFLAGS=-mmacosx-version-min=10.7 -c -Wall -O2 -funsigned-char -Wno-write-strings -Wno-char-subscripts 
endif

INCLUDEDIRS=
SOURCES=constructCode.cpp evserver.cpp csocket.cpp cs_ev.c debugger.cpp dictionarySystem.cpp englishTagger.cpp factSystem.cpp  functionExecute.cpp english.cpp infer.cpp mainSystem.cpp markSystem.cpp os.cpp outputSystem.cpp patternSystem.cpp readrawdata.cpp scriptCompile.cpp spellcheck.cpp systemVariables.cpp tagger.cpp testing.cpp textUtilities.cpp tokenSystem.cpp topicSystem.cpp userCache.cpp userSystem.cpp variableSystem.cpp
OBJECTS=$(SOURCES:.cpp=.o)
EXECUTABLE=ChatScript

all: $(SOURCES) binary

server: DEFINES+= -DLOCKUSERFILE=1 -DEVSERVER=1 -DEVSERVER_FORK=1 -DDISCARDDATABASE=1
server: PGLOAD= -pthread
server: INCLUDEDIRS=-I../lib/libev
server: all

pgserver: DEFINES+= -DLOCKUSERFILE=1 -DEVSERVER=1 -DEVSERVER_FORK=1 
pgserver: PGLOAD= -lpq -pthread
pgserver: INCLUDEDIRS=-I../lib/libev
pgserver: all


clean:
	-rm -f $(EXECUTABLE)
	-rm -f ../$(EXECUTABLE)
	-rm -f *.o

binary: $(OBJECTS)
	$(CC) $(OBJECTS) $(LDFLAGS) $(DEFINES) $(INCLUDEDIRS) -o $(EXECUTABLE)
	cp $(EXECUTABLE) ..

.cpp.o:
	$(CC) $(CFLAGS) $(DEFINES) $(INCLUDEDIRS) $< -o $@
