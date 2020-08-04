DEFS = -DCONFDIR=\"${sysconfdir}/\" -DBINDIR=\"${bindir}/\" @DEFS@
INCLUDES = -I$(top_srcdir)/include
LIBS =

man8_MANS = $(top_srcdir)/doc/ircd.8
EXTRA_DIST = $(man8_MANS)

bin_PROGRAMS = ircd
ircd_SOURCES = channel.c  date.c  ircd.c  list.c  server.c  s_msg.c  s_numeric.c  s_sys.c
ircd_LDADD =$(top_srcdir)/lib/libirc.a

install-data-local:
	@if test ! -d "$(DESTDIR)/${sysconfdir}"; then mkdir -p $(DESTDIR)/${sysconfdir}; fi;
	@echo "Installing configuration file in $(DESTDIR)/${sysconfdir}";
	@$(INSTALL_DATA) ../doc/example.conf $(DESTDIR)/${sysconfdir}/example.conf;

clean-generic:
	-rm -f .#* *~

