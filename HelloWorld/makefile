PROJECT_NAME = HelloWorld
_DEPS = HelloWorld.h
_OBJ = main.o HelloWorld.o 

IDIR = include
SDIR = src
ODIR = build
LDIR = lib
BDIR = bin

CC = g++
CFLAGS=-I $(IDIR)

#LIBS=-lm

DEPS = $(patsubst %,$(IDIR)/%,$(_DEPS))
OBJ = $(patsubst %,$(ODIR)/%,$(_OBJ))


$(ODIR)/%.o: src/%.cpp $(DEPS)
	mkdir -p build
	$(CC) -c -o $@ $< $(CFLAGS)

$(PROJECT_NAME) : $(OBJ)
	mkdir -p bin
	$(CC) -o $(BDIR)/$@ $^ $(CFLAGS) 
	#$(LIBS)

.PHONY: clean

clean:
	rm -f $(ODIR)/*.o *~ core $(INCDIR)/*~ 
