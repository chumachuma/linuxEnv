PROJECT_NAME = $(TYPE_PREFIX)$(notdir $(shell pwd))$(TYPE_SUFFIX)

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
CFLAGS=-I$(IDIR) -Wall -Wextra $(BUILD_TYPE) $(LIBS) $(LIBS_DIR) $(INCDIR) $(DEFINES)
DEPFLAGS = -MT $@ -MMD -MP -MF $(DDIR)/$*.td

SHELL = /bin/sh
.SUFFIXES:
.SUFFIXES: .cpp .o .d .td

LIBS = #-l 
LIBS_DIR = #-L
INCLUDES = #-I
DEFINES = #-D

TEST_EXE = $(EXE)
TEST_ARG = 

-include MakeSpec.mk

.PHONY: all
all: $(EXE)
#all should be debug

.PHONY: install
install: $(EXE)
install: check 
	echo TODO install application in right places and if exists run a test

.PHONY: debug
debug: BUILD_TYPE = -D_DEBUG -g
debug: TYPE_SUFFIX = D
debug: all

.PHONY: sharedArchive
sharedArchive: TYPE_PREFIX ::=lib
sharedArchive: TYPE_SUFFIX ::=.a
sharedArchive:
	echo $(EXE)

.PHONY: sharedArchive
sharedObject: TYPE_PREFIX ::=lib
sharedObject: TYPE_SUFFIX ::=.so
sharedObject:
	echo $(EXE)

$(EXE): $(OBJ) | $(BDIR)
	$(CC) -o $(BDIR)/$(PROJECT_NAME) $^ $(CFLAGS)

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
	$(TEST_EXE) $(TEST_ARG)

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
