dnl *
dnl *
dnl *  System        : 
dnl *  Module        : 
dnl *  Object Name   : $RCSfile$
dnl *  Revision      : $Revision$
dnl *  Date          : $Date$
dnl *  Author        : $Author$
dnl *  Created By    : Robert Heller
dnl *  Created       : Sat Apr 13 13:06:21 2024
dnl *  Last Modified : <240413.1338>
dnl *
dnl *  Description	
dnl *
dnl *  Notes
dnl *
dnl *  History
dnl *	
dnl *  $Log$
dnl *
dnl *------------------------------------------------------------------
dnl *
dnl *    Copyright (C) 2024  Robert Heller D/B/A Deepwoods Software
dnl *			51 Locke Hill Road
dnl *			Wendell, MA 01379-9728
dnl *
dnl *    This program is free software; you can redistribute it and/or modify
dnl *    it under the terms of the GNU General Public License as published by
dnl *    the Free Software Foundation; either version 2 of the License, or
dnl *    (at your option) any later version.
dnl *
dnl *    This program is distributed in the hope that it will be useful,
dnl *    but WITHOUT ANY WARRANTY; without even the implied warranty of
dnl *    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
dnl *    GNU General Public License for more details.
dnl *
dnl *    You should have received a copy of the GNU General Public License
dnl *    along with this program; if not, write to the Free Software
dnl *    Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.
dnl *
dnl * 
dnl *
dnl *------------------------------------------------------------------


AC_INIT([TkGCal],[0.0.0],[support@deepsoft.com],[TkGCal])
AC_CANONICAL_BUILD
AC_CANONICAL_HOST
AC_SUBST(build)
AC_CANONICAL_TARGET
AC_SUBST(target)
AC_CONFIG_SRCDIR([TkGCal.tcl.in])
AM_INIT_AUTOMAKE
AC_CONFIG_MACRO_DIR([m4])

if test "x${prefix}" = "xNONE"; then
    prefix=/usr/local
    fi
    if test "x${exec_prefix}" = "xNONE"; then
        exec_prefix="${prefix}"
        fi
        
BUILD_DIR=`pwd`
TOP_DIR=${BUILD_DIR}

AC_SUBST(TOP_DIR)
AC_SUBST(BUILD_DIR)

srcdir=`dirname $0`
cd $srcdir
SRC_DIR=`pwd`
cd $BUILD_DIR

AC_SUBST(SRC_DIR)

AC_SUBST(target)

AC_USE_SYSTEM_EXTENSIONS

AX_PKG_DOXYGEN(1.6.0, [], [ AC_MSG_ERROR([DOXYGEN 1.6.0 is required to build.]) ])

AC_PATH_PROG(GCALCLI,gcalcli)

AC_PATH_PROG(HOSTTCLSH,tclsh8.6,tclsh)

AX_SNIT

AC_PATH_PROGS(UNZIP,unzip)

AC_MSG_CHECKING([Checking target tclkit])
case $target_os in 
  macos | darwin*) 
    dnl AC_MSG_ERROR([Unsupported target OS: MacOSX -- see the READMEs for info on how to build for MacOSX])
    AC_SUBST(TCLKITRUN, tclkit-8.6.13-Darwin-Img1.4.14)
    AC_SUBST(NEED_APP_BUNDLE,[true])
    AC_SUBST(BINTRUE,[/usr/bin/true])
    ;;
  linux-gnu*)
    case $target_cpu in
      x86_64)
	AC_SUBST(TCLKITRUN, [tclkit-8.6.11-x86_64-Img1.4.7])
	;;
      i*86)
	AC_SUBST(TCLKITRUN, [tclkit-8.6.11-i386-Img1.4.7])
	;;
      arm*)
        AC_SUBST(TCLKITRUN, [tclkit-8.6.11-armv7l-Img1.4.8])
        ;;
      aarch64)
        AC_SUBST(TCLKITRUN, [tclkit-8.6.10-aarch64-Img1.4.14])
        ;;
      *)
	AC_MSG_ERROR([Unsupported Linux arch: $target_cpu])
	;;
     esac
     dnl AC_SUBST(KIT_EXTRA_CFLAGS,[])
     AC_SUBST(NEED_APP_BUNDLE,[false])
     AC_SUBST(BINTRUE,[/bin/true])
     ;;

   mingw* | winnt | windows* | cygwin)
     AC_MSG_ERROR([Unsupported target OS: MS-Windows.  See the READMEs for info about building for MS-Windows])
     dnl AC_SUBST(TCLKITRUN, tclkit-win32.exe)
     dnl AC_SUBST(EXEEXT, .exe)
     dnl AC_SUBST(NEED_APP_BUNDLE,[false])
     dnl AC_SUBST(BINTRUE,[/bin/true])
     ;;
   *) 
     AC_MSG_ERROR([Unsupported Operating System: $target_os])
     ;;
esac

AC_MSG_RESULT([TCLKITRUN is $TCLKITRUN])
AM_CONDITIONAL(MACOSX, test x${NEED_APP_BUNDLE} = xtrue)                        

AC_PATH_PROG(PDFLATEX,pdflatex,$BINTRUE)
AC_PATH_PROG(LATEX,latex,$BINTRUE)
AC_PATH_PROG(MAKEINDEX,makeindex,$BINTRUE)
AC_PATH_PROG(BIBTEX,bibtex,$BINTRUE)
AC_PATH_PROG(DVIPS,dvips,$BINTRUE)
AC_PATH_PROG(PS2PDF,ps2pdf,$BINTRUE)

AC_MSG_CHECKING([Checking build tclkit])
case $build_os in
  macos | darwin*)
    dnl AC_MSG_ERROR([Unsupported build OS: MacOSX -- see the READMEs for info on how to build on MacOSX])
    AC_SUBST(BEXEEXT, )
    AC_SUBST(TCLKITBSRC, tclkit-8.6.13-Darwin-Img1.4.14)
    ;;
  linux-gnu*)
    AC_SUBST(BEXEEXT, )
    case $build_cpu in
      x86_64)
        AC_SUBST(TCLKITBSRC, [tclkit-8.6.11-x86_64-Img1.4.7])
        ;;
      i*86)
        AC_SUBST(TCLKITBSRC, [tclkit-8.6.11-i386-Img1.4.7])
        ;;
      arm*)
        AC_SUBST(TCLKITBSRC, [tclkit-8.6.11-armv7l-Img1.4.8])
        ;;
      aarch64)
        AC_SUBST(TCLKITBSRC, [tclkit-8.6.10-aarch64-Img1.4.14])
        ;;
      *)
        AC_MSG_ERROR([Unsupported Linux arch: $build_cpu])
        ;;
    esac
    ;;
  mingw* | winnt | windows* | cygwin)
    AC_MSG_ERROR([Unsupported build OS: MS-Windows.  See the READMEs for info about building on MS-Windows])
    dnl AC_SUBST(BEXEEXT, [.exe])
    dnl AC_SUBST(TCLKITBSRC, )
    ;;
  *)
    AC_MSG_ERROR([Unsupported Operating System: $build_os])
    ;;
esac
      
AC_MSG_RESULT([TCLKITBSRC is $TCLKITBSRC])

AC_PATH_PROG(SED,sed)

AC_CONFIG_FILES([Makefile \
		 BuildScripts/Makefile \
		 BuildData/Makefile \
		 Scripts/Makefile \
		 TkGCal.tcl])
AC_CONFIG_COMMANDS([default])
AC_OUTPUT
