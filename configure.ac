AC_PREREQ(2.64)

AC_INIT([dnstap-ldns],
        [0.2.0],
        [https://github.com/dnstap/dnstap-ldns/issues],
        [dnstap-ldns],
        [https://github.com/dnstap/dnstap-ldns])

AC_CONFIG_SRCDIR([dnstap-ldns.c])
AC_CONFIG_AUX_DIR([build-aux])
AM_INIT_AUTOMAKE([foreign 1.11 -Wall -Wno-portability silent-rules subdir-objects])
AC_PROG_CC_STDC
AC_USE_SYSTEM_EXTENSIONS
AC_SYS_LARGEFILE
AC_CONFIG_MACRO_DIR([m4])
AM_SILENT_RULES([yes])

my_CFLAGS="-Wall \
-Wmissing-declarations -Wmissing-prototypes \
-Wnested-externs -Wpointer-arith \
-Wpointer-arith -Wsign-compare -Wchar-subscripts \
-Wstrict-prototypes -Wshadow \
-Wformat-security"
AC_SUBST([my_CFLAGS])

AC_MSG_CHECKING([build with debug output])
AC_ARG_ENABLE([debug],
              [AS_HELP_STRING([--enable-debug],
                              [enable debug output [default=no]])],
                              [debug_enabled="$enableval"],
                              [debug_enabled=no])
AC_MSG_RESULT([$debug_enabled])

if test x"$debug_enabled" != x"yes"; then
    AC_DEFINE([NDEBUG], [1], [liblogfaf no debug output])
fi

AC_CONFIG_HEADERS(config.h)
AC_CONFIG_FILES([Makefile])

PKG_CHECK_MODULES([libldns], [libldns])

PKG_CHECK_MODULES([libfstrm], [libfstrm >= 0.6.0])

PKG_CHECK_MODULES([libprotobuf_c], [libprotobuf-c >= 1.0.1])

PKG_CHECK_MODULES([libevent], [libevent])

AC_PATH_PROG([PROTOC_C], [protoc-c])
AS_IF([test -z "$PROTOC_C"],
  AC_MSG_ERROR([The protoc-c program was not found. Please install the protobuf-c compiler!]))

AC_OUTPUT
AC_MSG_RESULT([
    $PACKAGE $VERSION

        compiler:               ${CC}
        cflags:                 ${CFLAGS}
        ldflags:                ${LDFLAGS}
        libs:                   ${LIBS}

        prefix:                 ${prefix}
        sysconfdir:             ${sysconfdir}
        libdir:                 ${libdir}
        includedir:             ${includedir}
])
