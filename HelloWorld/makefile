CC = g++ #compiler to use
CFLAGS = -I. #flags to pass to compilation command
DEPS = HelloWorld.h
OBJ = main.cpp HelloWorld.cpp

%.o: %.c $(DEPS)
	$(CC) -c -o $@ $< $(CFLAGS)
	#recompile .o in header changes

HelloWorld: main.o HelloWorld.o
#HelloWorld rule needs to be executed if main.cpp is changed
	$(CC) -o HelloWorld main.o HelloWorld.o -I.
	#g++ -o outputName inputFiles -I includeDirectories
