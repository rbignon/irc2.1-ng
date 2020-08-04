#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.61)
AC_INIT(oldirc, 2.1.1-ng, romain@symlink.me)
AC_CONFIG_SRCDIR([server/ircd.c])
AC_CONFIG_HEADER([config.h])

AM_INIT_AUTOMAKE([foreign 1.5])

# Checks for programs.
AC_PROG_CC
AC_PROG_MAKE_SET
AC_PROG_RANLIB

# Checks for libraries.
AC_CHECK_LIB([curses], [main])
AC_CHECK_LIB([termcap], [main])

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([arpa/inet.h fcntl.h netdb.h netinet/in.h sgtty.h stdlib.h string.h strings.h sys/file.h sys/ioctl.h sys/socket.h sys/time.h utmp.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_TIME
AC_STRUCT_TM

# Checks for library functions.
AC_FUNC_FORK
AC_PROG_GCC_TRADITIONAL
AC_FUNC_MALLOC
AC_FUNC_SELECT_ARGTYPES
AC_FUNC_SETPGRP
AC_FUNC_SETVBUF_REVERSED
AC_TYPE_SIGNAL
AC_CHECK_FUNCS([alarm dup2 gethostbyaddr gethostbyname gethostname gettimeofday inet_ntoa isascii select socket strchr strrchr])

AC_ARG_ENABLE(  server,
                [AC_HELP_STRING([--enable-server],[compilation of IRCD server])],
                [
                        if test "x${enableval}" != "xno"; then
                                INSTALL_SERVER=server
                                AC_SUBST(INSTALL_SERVER)
                        fi
                ],
        )

AC_ARG_ENABLE(  services,
                [AC_HELP_STRING([--enable-services],[compilation of IRC Services])],
                [
                        if test "x${enableval}" != "xno"; then
                                INSTALL_SERVICES=services
                                AC_SUBST(INSTALL_SERVICES)
                        fi
                ],
        )

AC_ARG_ENABLE(  client,
                [AC_HELP_STRING([--enable-client],[compilation of IRC Client])],
                [
                        if test "x${enableval}" != "xno"; then
                                INSTALL_CLIENT=client
                                AC_SUBST(INSTALL_CLIENT)
                        fi
                ],
        )



#  WARNINGS
AC_ARG_ENABLE(  warnings,
                [AC_HELP_STRING([--enable-warnings],[enable warnings during compilation (-Wall)])],
                [
                        if test "x${enableval}" != "xno"; then
                                WARNINGS=1
                        fi
                ],
                )

#  DEBUG
AC_ARG_ENABLE(  debug,
                [AC_HELP_STRING([--enable-debug],[enable debug])],
                [
                        if test "x${enableval}" != "xno"; then
                                DEBUG=1
                        fi
                ],
                [DEBUG=0 ]
        )


if test "x$GCC" = "xyes"; then
    dnl get gcc version
    AC_MSG_CHECKING([gcc version])
            gccver=$($CC -dumpversion)
            gccvermajor=$(echo $gccver | cut -d . -f1)
            gccverminor=$(echo $gccver | cut -d . -f2)
            gccvernum=$(expr $gccvermajor "*" 100 + $gccverminor)
    AC_MSG_RESULT($gccver)

    if test "x${WARNINGS}" = "x1"; then
      dnl Enable all warnings
# en reserve: -Weffc++ (il fait bien mal aux variables non initialisées)
#             -pedantic (il trouve rien à part une répétition de ;; dans SDL_ttf.h)
#             -Wold-style-cast (prohibe les anciens styles de conversions)
      GCC_FLAGS="-Wall"
      #CFLAGS="$CFLAGS -D_GNU_SOURCE=1 -std=c99"
      CXXFLAGS="$CXXFLAGS -Wstrict-null-sentinel -ansi"

      dnl Enable *more* warnings
      if test "$gccvernum" -ge "400"; then
                  dnl gcc 4.0 or later
          GCC_FLAGS="$GCC_FLAGS -Wextra"
      else
          GCC_FLAGS="$GCC_FLAGS -W"
      fi

      dnl Skip 'unused parameter' warning
      GCC_FLAGS="$GCC_FLAGS -Wno-unused-parameter"
    fi

    if test "x${DEBUG}" = "x1"; then
        GCC_FLAGS="$GCC_FLAGS -O0 -g -DDEBUG"
    else
        GCC_FLAGS="$GCC_FLAGS -O2"
    fi

    CFLAGS="$CFLAGS $GCC_FLAGS"
    CXXFLAGS="$CXXFLAGS $GCC_FLAGS"
else
    if test "x${DEBUG}" = "x1"; then
        CFLAGS="$CFLAGS -DDEBUG"
        CXXFLAGS="$CXXFLAGS -DDEBUG"
    fi
fi

AC_CONFIG_FILES([Makefile lib/Makefile services/Makefile server/Makefile client/Makefile])

AC_OUTPUT
