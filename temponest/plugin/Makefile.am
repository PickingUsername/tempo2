plugindir=@TEMPO2_PLUG_INSTALL@
###
#
# This sets the includes and options that are needed to build nice modules with libtool
#
###
LDFLAGS+= -shared -module -avoid-version -shrext .t2
AM_CPPFLAGS=-I@top_srcdir@/ -I@top_srcdir@/temponest

# These are the plugins we will build here
PLUGINS=
plugin_LTLIBRARIES =


if HAVE_MULTINEST

include ../temponest.am

temponest_@T2ARCH@_plug_la_SOURCES = TempoNestPlugin.cpp
temponest_@T2ARCH@_plug_la_LIBADD = ../$(tnlib_libadd) $(tnlib_ldflags)
temponest_@T2ARCH@_plug_la_INCLUDES = $(tnlib_includes)
PLUGINS+= temponest
plugin_LTLIBRARIES+= temponest_@T2ARCH@_plug.la

endif

install: temponest_@T2ARCH@_plug.la plugdir
	$(INSTALL) .libs/temponest_@T2ARCH@_plug.t2 $(plugindir)

plugdir:
	mkdir -p $(plugindir)
