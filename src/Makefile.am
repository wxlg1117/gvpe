## Produce this file with automake to get Makefile.in

#SUBDIRS = rohc

sbin_PROGRAMS = gvpe
bin_PROGRAMS = gvpectrl

EXTRA_DIST = device-linux.C device-cygwin.C device-tincd.C device-darwin.C callback.pl	\
   tincd/apply tincd/fixit	\
   tincd/cygwin/device.c tincd/darwin/device.c tincd/freebsd/device.c	\
   tincd/linux/device.c tincd/mingw/common.h tincd/mingw/device.c tincd/netbsd/device.c	\
   tincd/openbsd/device.c tincd/raw_socket/device.c tincd/solaris/device.c \
   tincd/uml_socket/device.c tincd/bsd/device.c \
   ether_emu.C lzf/lzf_c.c lzf/lzf_d.c

INCLUDES = -I$(top_builddir) -I$(top_srcdir)/lib -I$(top_srcdir)/libev @INCLUDES@

LIBS = @LIBS@ @LIBINTL@

if ROHC
ROHCLIB = rohc/librohc.a
else
ROHCLIB =
endif

COMMON = global.h conf.h conf.C util.h util.C \
         slog.h slog.C netcompat.h ev_cpp.h ev_cpp.C 

gvpe_SOURCES = gvpe.C vpn.h vpn.C vpn_tcp.C vpn_dns.C \
               sockinfo.h sockinfo.C \
               lzf/lzf.h lzf/lzfP.h \
               connection.h connection.C callback.h device.h device.C \
               $(COMMON)
gvpe_LDADD = $(top_builddir)/lib/libgvpe.a $(ROHCLIB)
gvpe_LDFLAGS = @LDFLAGS_DAEMON@

gvpectrl_SOURCES = gvpectrl.C $(COMMON)
gvpectrl_LDADD = $(top_builddir)/lib/libgvpe.a

localedir = $(datadir)/locale

DEFINES = -DPKGLIBDIR=$(pkglibdir) -DCONFDIR=\"$(sysconfdir)\"	\
	  -DLOCALEDIR=\"$(localedir)\" -DLOCALSTATEDIR=\"$(localstatedir)\" \
          -DIFTYPE_@IFTYPE@=1 -DIF_@IFSUBTYPE@=1

AM_CFLAGS = $(DEFINES)
AM_CXXFLAGS = $(DEFINES)

dist-hook:
	rm -f `find . -type l`

