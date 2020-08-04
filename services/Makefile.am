DEFS = -DCONFDIR=\"${sysconfdir}/\" -DBINDIR=\"${bindir}/\" -DAUTOMATON @DEFS@
INCLUDES = -I$(top_srcdir)/include

bin_PROGRAMS = gm dip

D=../client

IRCOBJ= $D/str.c $D/ignore.c $D/help.c $D/c_numeric.c $D/client.c

LOC = $D/c_msg.c  $D/irc.c $D/c_sys.c

AOBJ = $(IRCOBJ) $(LOC)

gm_SOURCES = $(AOBJ) wumpus.c
dip_SOURCES = $(AOBJ) diplomacy.c

gm_LDADD =$(top_srcdir)/lib/libirc.a
dip_LDADD =$(top_srcdir)/lib/libirc.a

