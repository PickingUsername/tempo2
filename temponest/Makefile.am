###
#
# This sets the includes and options that are needed to build nice modules with libtool
#
###
LDFLAGS+= -shared
AM_CPPFLAGS=-I@top_srcdir@/

# For now, TempoNest only works if MultiNest is installed
# TODO: likelihoods and all should work without MultiNest as well

if HAVE_MULTINEST

bin_PROGRAMS =
lib_LTLIBRARIES = libtemponest.la
noinst_LTLIBRARIES = libtemponestcore.la

include temponest.am

libtemponestcore_la_SOURCES = $(tncore_sources)
libtemponestcore_la_LIBADD = $(tncore_libadd) $(tncore_ldflags)
libtemponestcore_la_LDFLAGS = $(tncore_libadd) $(tncore_ldflags)
libtemponestcore_la_CFLAGS = -fPIC
libtemponestcore_la_INCLUDES = $(tncore_includes)
libtemponestcore_la_includedir = $(includedir)
libtemponestcore_la_include_HEADERS = $(tncore_headers)

libtemponest_la_SOURCES = $(tnlib_sources)
libtemponest_la_LIBADD = $(tnlib_libadd) $(tnlib_ldflags)
libtemponest_la_LDFLAGS = $(tnlib_libadd) $(tnlib_ldflags)
libtemponest_la_CFLAGS = -fPIC
libtemponest_la_INCLUDES= $(tnlib_includes)

endif


########################################################################
##################### FROM HERE, BUILD THE PLUGIN ######################
########################################################################

plugindir=@TEMPO2_PLUG_INSTALL@
###
#
# This sets the includes and options that are needed to build nice modules with libtool
#
###
LDFLAGS+= -module -avoid-version -shrext .t2
AM_CPPFLAGS += -I@top_srcdir@/temponest

# These are the plugins we will build here
PLUGINS=
plugin_LTLIBRARIES =


if HAVE_MULTINEST

temponest_@T2ARCH@_plug_la_SOURCES = plugin/TempoNestPlugin.cpp
temponest_@T2ARCH@_plug_la_LIBADD = $(tnlib_libadd) $(tnlib_ldflags)
temponest_@T2ARCH@_plug_la_INCLUDES = $(tnlib_includes)
PLUGINS+= temponest
plugin_LTLIBRARIES+= temponest_@T2ARCH@_plug.la

endif

.PHONY: temponest-install

temponest-install: plugin plugdir install
	$(INSTALL) .libs/temponest_@T2ARCH@_plug.t2 $(plugindir)

plugdir:
	mkdir -p $(plugindir)
