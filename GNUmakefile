# $Header: /usr/cvs/Public/pygresql/module/GNUmakefile,v 1.19 2005-01-11 12:13:38 darcy Exp $
# $Id$

subdir = src/interfaces/python
top_builddir = ../../..
include $(top_builddir)/src/Makefile.global

NAME = _pgmodule
OBJS = pgmodule.o
SHLIB_LINK = $(libpq)
ifeq ($(PORTNAME), cygwin)
override CPPFLAGS += -DUSE_DL_IMPORT
SHLIB_LINK += $(python_libspec)
endif


include $(top_srcdir)/src/Makefile.shlib

override CPPFLAGS := -I$(libpq_srcdir) $(CPPFLAGS) $(python_includespec)

all: all-lib

all-lib: libpq-all

.PHONY: libpq-all
libpq-all:
	$(MAKE) -C $(libpq_builddir) all

install-warning-msg := { \
echo "*** Skipping the installation of the Python interface module for lack"; \
echo "*** of permissions.  To install it, change to the directory"; \
echo "***     `pwd`,"; \
echo "*** become the appropriate user, and do '$(MAKE) install'."; }

install: all installdirs
	@if test -w $(DESTDIR)$(python_moduleexecdir) && test -w $(DESTDIR)$(python_moduledir); then \
	  echo "$(INSTALL_SHLIB) $(shlib) $(DESTDIR)$(python_moduleexecdir)/_pgmodule$(DLSUFFIX)"; \
	  $(INSTALL_SHLIB) $(shlib) $(DESTDIR)$(python_moduleexecdir)/_pgmodule$(DLSUFFIX); \
	\
	  echo "$(INSTALL_DATA) $(srcdir)/pg.py $(DESTDIR)$(python_moduledir)/pg.py"; \
	  $(INSTALL_DATA) $(srcdir)/pg.py $(DESTDIR)$(python_moduledir)/pg.py; \
	\
	  echo "$(INSTALL_DATA) $(srcdir)/pgdb.py $(DESTDIR)$(python_moduledir)/pgdb.py"; \
	  $(INSTALL_DATA) $(srcdir)/pgdb.py $(DESTDIR)$(python_moduledir)/pgdb.py; \
	else \
	  $(install-warning-msg); \
	fi

installdirs:
	$(mkinstalldirs) $(DESTDIR)$(python_moduleexecdir) $(DESTDIR)$(python_moduledir)

uninstall:
	rm -f $(DESTDIR)$(python_moduleexecdir)/_pgmodule$(DLSUFFIX) \
	      $(DESTDIR)$(python_moduledir)/pg.py \
	      $(DESTDIR)$(python_moduledir)/pgdb.py

clean distclean maintainer-clean: clean-lib
	rm -f $(OBJS)