dnl Process this file with autoconf to produce a configure script.

AC_PREREQ(2.52)

AC_INIT([mate-system-monitor], [1.6.1],
        [http://www.mate-desktop.org/])
AC_CONFIG_SRCDIR(configure.ac)
AC_CONFIG_HEADERS(config.h)
AC_CONFIG_MACRO_DIR([m4])

AM_INIT_AUTOMAKE([no-dist-gzip dist-xz])
AC_SUBST(ACLOCAL_AMFLAGS, [\${ACLOCAL_FLAGS}])

AM_PROG_LIBTOOL

IT_PROG_INTLTOOL([0.35.0])
PKG_PROG_PKG_CONFIG([0.19])

AC_ISC_POSIX
AC_PROG_CC
AC_PROG_CXX
AC_LANG_CPLUSPLUS
AC_LANG_COMPILER_REQUIRE
AC_HEADER_STDC
MATE_COMPILE_WARNINGS

GLIB_REQUIRED=2.28.0
LIBWNCK_REQUIRED=2.5.0
LIBGTOP_REQUIRED=2.23.1
GTK_REQUIRED=2.20.0
MATE_ICON_THEME_REQUIRED=1.1.0
GTKMM_REQUIRED=2.22
GIOMM_REQUIRED=2.26.0
GLIBMM_REQUIRED=2.22
LIBXML_REQUIRED=2.0
RSVG_REQUIRED=2.12
DBUS_REQUIRED=0.7

PKG_CHECK_MODULES(GMODULE,gmodule-2.0,[GMODULE_ADD="gmodule-2.0"],[GMODULE_ADD=""])
PKG_CHECK_MODULES(PROCMAN,$GMODULE_ADD glib-2.0 >= $GLIB_REQUIRED libgtop-2.0 >= $LIBGTOP_REQUIRED libwnck-1.0 >= $LIBWNCK_REQUIRED gtk+-2.0 >= $GTK_REQUIRED mate-icon-theme >= $MATE_ICON_THEME_REQUIRED gtkmm-2.4 >= $GTKMM_REQUIRED libxml-2.0 >= $LIBXML_REQUIRED librsvg-2.0 >= $RSVG_REQUIRED glibmm-2.4 >= $GLIBMM_REQUIRED giomm-2.4 >= $GIOMM_REQUIRED dbus-glib-1 >= $DBUS_REQUIRED)


AC_ARG_ENABLE(more-warnings,
[AC_HELP_STRING([--enable-more-warnings], [Maximum compiler warnings])],
set_more_warnings="$enableval",[
    set_more_warnings=yes
])
AC_MSG_CHECKING(for more warnings, including -Werror)
if test "$GCC" = "yes" -a "$set_more_warnings" != "no"; then
    AC_MSG_RESULT(yes)
    CFLAGS="\
    -Wall \
    -Winline \
    -Wchar-subscripts -Wmissing-declarations -Wmissing-prototypes \
    -Wnested-externs -Wpointer-arith \
    -Wcast-align -Wsign-compare \
    -std=gnu89 \
    $CFLAGS"
    CXXFLAGS="-Wall -std=c++98 $CXXFLAGS"
else
    AC_MSG_RESULT(no)
fi

dnl CXXFLAGS="-fvisibility=hidden -fvisibility-inlines-hidden $CXXFLAGS"
dnl CXXFLAGS="-fvisibility-inlines-hidden $CXXFLAGS"

GLIB_GSETTINGS

GETTEXT_PACKAGE=mate-system-monitor
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE,"$GETTEXT_PACKAGE",
                   [The gettext catalog name])
AM_GLIB_GNU_GETTEXT

YELP_HELP_INIT

dnl Set PACKAGE_LOCALE_DIR in config.h.
GLIB_DEFINE_LOCALEDIR(PACKAGE_LOCALE_DIR)


AC_CONFIG_FILES([
Makefile
src/Makefile
pixmaps/Makefile
po/Makefile.in
help/Makefile
mate-system-monitor.desktop.in
])

AC_OUTPUT

echo "

Configuration:

	Source code location:	${srcdir}
	C Compiler:		${CC}
	C++ Compiler:		${CXX}
	CFLAGS:			${CFLAGS}
	CXXFLAGS:		${CXXFLAGS}
	Maintainer mode:	${USER_MAINTAINER_MODE}
	Languages:		${ALL_LINGUAS}
"
