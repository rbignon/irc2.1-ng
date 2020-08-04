DEFS = -DCONFDIR=\"${sysconfdir}/\" -DBINDIR=\"${bindir}/\" @DEFS@
INCLUDES = -I$(top_srcdir)/include

man1_MANS = $(top_srcdir)/doc/irc.1
EXTRA_DIST = $(man1_MANS)

bin_PROGRAMS = irc
irc_SOURCES = client.c  c_msg.c  c_numeric.c  c_sys.c  edit.c  help.c  ignore.c  irc.c  screen.c  str.c  swear.c

irc_LDADD =$(top_srcdir)/lib/libirc.a

clean-generic:
	-rm -f .#* *~

