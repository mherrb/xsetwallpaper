#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.69])
AC_INIT([xsetwallpaper], [0.2.0], [tobias@stoeckmann.org])
AC_CONFIG_SRCDIR([Makefile.am])
AC_CONFIG_HEADERS([config.h])

# Checks for programs.
AC_PROG_CC

# Initialize Automake
AM_INIT_AUTOMAKE([foreign])

# Check for pkg-config packages
PKG_CHECK_MODULES(PIXMAN, [pixman-1 >= 0.32])
PKG_CHECK_MODULES(PNG, [libpng >= 1.2])
PKG_CHECK_MODULES(XCB, [xcb-image >= 0.4 xcb-util >= 0.4])

# Check for OpenBSD's pledge(2)
AC_CHECK_FUNCS([pledge])

# Check if RandR support is requested
AC_MSG_CHECKING(whether RandR support is requested)
AC_ARG_WITH([randr],
  [AS_HELP_STRING([--without-randr], [disable RandR support])],
  [
   if test "$withval" = no ; then
     randr_support=no
   else
     randr_support=yes
   fi
  ],
  [ randr_support=auto ]
)
AC_MSG_RESULT($randr_support)
if test "$randr_support" != no ; then
  PKG_CHECK_MODULES(RANDR, xcb-randr >= 1.11, [randr_ok="yes"], [randr_ok="no"])
else
  randr_ok="no"
fi
AS_IF([test "$randr_ok" = yes],
  [AC_DEFINE(WITH_RANDR,[],[With RandR support])],[]
)
AM_CONDITIONAL(BUILD_RANDR, [test "$randr_ok" = yes])

# Check if JPEG support is requested
AC_MSG_CHECKING(whether JPEG support is requested)
AC_ARG_WITH([jpeg],
  [AS_HELP_STRING([--without-jpeg], [disable JPEG support])],
  [
   if test "$withval" = no ; then
     jpeg_support=no
   else
     jpeg_support=yes
   fi
  ],
  [ jpeg_support=auto ]
)
AC_MSG_RESULT($jpeg_support)
if test "$jpeg_support" != no ; then
  PKG_CHECK_MODULES(JPEG, libjpeg >= 1.5, [jpeg_ok="yes"], [jpeg_ok="no"])
else
  jpeg_ok="no"
fi
AS_IF([test "$jpeg_ok" = yes],
  [AC_DEFINE(WITH_JPEG,[],[With JPEG support])],[]
)
AM_CONDITIONAL(BUILD_JPEG, [test "$jpeg_ok" = yes])

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
