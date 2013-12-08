
UNITNAME=cppunit
INCLUDEDIRS=../../include
MYCPPFLAGS=-EHsc
INSTALL=../../../lib

CC=cl -nologo
CXX=cl
AR=lib

SRCS=$(wildcard *.cpp)
OBJS=$(SRCS:.cpp=.o)
MKDIR=mkdir -p
CP=cp

LIBNAME=lib$(UNITNAME)$(ADD_D).a
PDBNAME=$(basename $(LIBNAME)).pdb

CPPFLAGS=$(MYCPPFLAGS) $(CPPINCLUDES) $(OPTCPPFLAGS) $(DBGCPPFLAGS)

CPPINCLUDES=$(addprefix -I, $(INCLUDEDIRS))

ifneq ($(DEBUG),) # Settings for the debug builds
  OPTCPPFLAGS=
  DBGCPPFLAGS=-Zi
  ADD_D=d
else              # Settings for the release builds
  OPTCPPFLAGS=-O2
  DBGCPPFLAGS=-Zi 
  ADD_D=
endif

%.o : %.cpp
	$(CC) -c $(CFLAGS) $(CPPFLAGS) $< -Fo$@ -Fd$(PDBNAME)

# Targets start here.
default: $(LIBNAME)

$(LIBNAME) : $(OBJS)
	$(AR) -out:$@ $(OBJS)

clean:
	$(RM) $(LIBNAME) $(PDBNAME) $(OBJS)

depend:
	$(CC) $(CFLAGS) -MM *.cpp

$(INSTALL)/$(LIBNAME) : $(LIBNAME)
	$(MKDIR) $(INSTALL)
	$(CP) $(LIBNAME) $(PDBNAME) $(INSTALL)

install: $(INSTALL)/$(LIBNAME)

# list targets that do not create files
.PHONY: default clean depend install
