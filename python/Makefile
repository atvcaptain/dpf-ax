# Cygwin/Linux-GCC Makefile
#
# $Id: Makefile 301 2010-09-30 13:09:13Z strubi $
#
# This is the GNU Makefile to create:
# - a Python module for the API tester
#

DEVLIB  = ..

############################################################################
# Configure these to your needs
LIBNAME = dpf
DLLCSRCS =
COMMONSRCDIR = $(DEVLIB)/python
DLLINSTALLDIR = ../$(CONFIG)
DLLCOMMONSRCS = py_device.c
DEBUGOPTS = -g

ifdef DEBUG
	DEBUGOPTS += -DDEBUG
endif

CLIENTLIB = -L$(DEVLIB)/dpflib -ldpf -lusb

############################################################################

MODULENAME = $(LIBNAME)

ifndef PLATFORM
PLATFORM=$(shell "uname")
endif

ifneq (Linux, $(PLATFORM))
CLIENTLIB += -lsgutils2
endif


include $(DEVLIB)/unixdll.mk
DLLDEPS = $(CLIENTLIB) -lpython3.8
PYTHONINCLUDES = -I${PYTHON_INCLUDE_DIR}


INCLUDES = -I$(DEVLIB)/include -I$(DEVLIB)/dpflib
INCLUDES += $(PYTHONINCLUDES)

CFLAGS +=  -DMODULENAME=$(MODULENAME)
CFLAGS +=  -Wall

all: dll

install:: installdll
	@cp $(DLL) $(DLLINSTALLDIR)/$(INSTALLNAME)$(DLLEXT)
	@echo -------------------------------------------------------------------
	@echo Python module installed in:
	@echo `pwd`/$(DLLINSTALLDIR)/$(INSTALLNAME)$(DLLEXT)
	@echo -------------------------------------------------------------------
	@echo

