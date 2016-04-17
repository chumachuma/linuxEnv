PROJECT_NAME = $(notdir $(shell pwd))

IDIR = include
SDIR = src
ODIR = build
DDIR = $(ODIR)/dependecies
SRC  = $(wildcard $(SDIR)/*.cpp)
OBJ  = $(subst $(SDIR)/, $(ODIR)/, $(SRC:.cpp=.o))
EXE  = $(BDIR)/$(PROJECT_NAME)
LDIR = lib
BDIR = bin

CC = g++
CFLAGS=-I$(IDIR)
DEPFLAGS = -MT $@ -MMD -MP -MF $(DDIR)/$*.td

#LIBS = -l 
#LIBS_DIR = -L
#RUN_TEST = $(BDIR)/$(PROJECT_NAME)

SHELL = /bin/sh
.SUFFIXES:
.SUFFIXES: .cpp .o .d .td

-include MakeSpec.mk

.PHONY: all
all: $(EXE)
#all should be debug

install: $(EXE)
	echo install application in right places and if exists run a test
	$(RUN_TEST)

$(EXE): $(OBJ) | $(BDIR)
	$(CC) -o $(BDIR)/$(PROJECT_NAME) $^ $(LIBS) $(CFLAGS)

debug: CFLAGS += -D_DEBUG -g
debug: all

$(ODIR)/%.o: src/%.cpp $(DDIR)/%.d | $(ODIR) $(DDIR)
	$(CC) -c -o $@ $< $(DEPFLAGS) $(CFLAGS)
	mv -f $(DDIR)/$*.td $(DDIR)/$*.d

$(BDIR):
	mkdir -p $(BDIR)

$(ODIR):
	mkdir -p $(ODIR)

$(DDIR): | $(ODIR)
	mkdir -p $(DDIR)

$(DDIR)/%.d: ;
.PRECIOUS: $(DDIR)/%.d

-include $(subst $(SDIR)/, $(DDIR)/, $(SRC:.cpp=.d))

.PHONY: TAGS
TAGS:
	ctags -R

.PHONY: info
info:
	echo TODO: generate infofile read MAKEINFO

.PHONY:dist
dist:
	echo TODO: generate tar file

.PHONY: check
check:
	echo TODO: run test on build not on install

.PHONY: clean
clean:
	-rm -f $(ODIR)/*.o $(EXE)* *~ core $(INCDIR)/*~ 

.PHONY: cleandep
cleandep:
	-rm -f $(DDIR)/*.d $(DDIR)/*.td

.PHONY: distclean
distclean: clean cleandep

.PHONY: help
help:
	@echo "all:                 Build all"
	@echo "debug:               Build project with debug information"
	@echo "dist:                Generate .tar file"
	@echo "check:               Run available test"
	@echo "TAGS:                Generate tags file. Requires ctags"
	@echo "info:                Generate info file"
	@echo "clean:               Clean project"
	@echo "cleandep:            Clean dependencies files"
	@echo "distclean:           Clean all generated files"
	@echo "help:                Show this help message. Make  <space> <tab>: shows all targets"
	@echo "maketest:            Used for Debug Makefile"

.PHONY: maketest
maketest:
	echo $(PROJECT_NAME)
	echo $(EXE)
