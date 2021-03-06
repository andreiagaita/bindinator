AC_INIT([bindinator], [1.0])
AC_CONFIG_SRCDIR([README.md])
AC_CANONICAL_TARGET
AM_INIT_AUTOMAKE([foreign])
AM_MAINTAINER_MODE
AC_PROG_INSTALL

AC_PATH_PROG(XSLTPROC, xsltproc, no)
if test "x$XSLTPROC" = "xno" ; then
	AC_MSG_ERROR([xsltproc not found])
fi
AC_SUBST(XSLTPROC)

AC_PATH_PROG(XMLLINT, xmllint, no)
if test "x$XMLLINT" = "xno" ; then
	AC_MSG_ERROR([xmllint not found. Install libxml2-utils to get it.])
fi
AC_SUBST(XMLLINT)

PKG_CHECK_MODULES(GIR, gobject-introspection-1.0, has_gir=true, has_gir=false)
if test "x$has_gir" = "xfalse"; then
	AC_MSG_ERROR([gobject-introspection not found, cannot determine gir directory. Install libgirepository1.0-dev to get it.])
fi

GIRDIR=`pkg-config --variable=girdir gobject-introspection-1.0`/
AC_SUBST(GIRDIR)

AC_PATH_PROG(GAPIFIXUP, gapi3-fixup, no)
if test "x$GAPIFIXUP" = "xno"; then
	AC_MSG_CHECKING(for gapi3-fixup.exe)
	GAPIFIXUP=`which gapi3-fixup.exe 2> /dev/null`
	if test "x$GAPIFIXUP" = "xno" ; then
		AC_MSG_ERROR(['gapi3_fixup'/'gapi3-fixup.exe' not found.])
	fi
	AC_MSG_RESULT($GAPIFIXUP)
	GAPIFIXUP="$MONO $GAPI_FIXUP"
fi
AC_SUBST(GAPIFIXUP)

AC_PATH_PROG(UUIDGEN, uuidgen, no)
if test "x$UUIDGEN" = "xno" ; then
	AC_MSG_ERROR([uuidgen not found. Install uuid-runtime to get it.])
fi
AC_SUBST(UUIDGEN)

AC_PATH_PROG(UNIX2DOS, unix2dos, [cat -])
if test "x$UNIX2DOS" = "xcat -" ; then
	AC_MSG_RESULT([unix2dos not found, using cat])
fi
AC_SUBST(UNIX2DOS)

AC_CONFIG_FILES([
	Makefile
	bindinate/Makefile
	bindinate/bindinate
	bindinate/gir2gapi.xslt
])
AC_CONFIG_COMMANDS([default],[[ echo timestamp > stamp-h ]],[[]])
AC_OUTPUT

cat <<EOF

Configuration summary
---------------------

   * Installation prefix: ${prefix}

EOF
