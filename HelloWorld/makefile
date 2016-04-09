CC = g++ #compiler to use
CFLAGS = -I. #flags to pass to compilation command
DEPS = HelloWorld.h
OBJ = main.o HelloWorld.o

%.o: %.c $(DEPS)
	$(CC) -c -o $@ $< $(CFLAGS)
	#recompile .o in header changes

HelloWorld: $(OBJ) 
#HelloWorld rule needs to be executed if main.cpp is changed
	$(CC) -o $@ $^ $(CFLAGS)
	#g++ -o outputName inputFiles -I includeDirectories

#$@ left of :
#$^ right  of :
#$< first item of dependecy list
