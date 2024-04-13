##-*- makefile -*-############################################################
#
#  System        : 
#  Module        : 
#  Object Name   : $RCSfile$
#  Revision      : $Revision$
#  Date          : $Date$
#  Author        : $Author$
#  Created By    : Robert Heller
#  Created       : Sat Apr 13 12:36:44 2024
#  Last Modified : <240413.1453>
#
#  Description	
#
#  Notes
#
#  History
#	
#  $Log$
#
##############################################################################
#
#    Copyright (C) 2024  Robert Heller D/B/A Deepwoods Software
#			51 Locke Hill Road
#			Wendell, MA 01379-9728
#
#    This program is free software; you can redistribute it and/or modify
#    it under the terms of the GNU General Public License as published by
#    the Free Software Foundation; either version 2 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU General Public License for more details.
#
#    You should have received a copy of the GNU General Public License
#    along with this program; if not, write to the Free Software
#    Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.
#
# 
#
##############################################################################

ACLOCAL_AMFLAGS = -I m4

SUBDIRS = BuildScripts BuildData Scripts

EXTRA_DIST = bootstrap TkGCal.tcl.in

bin_SCRIPTS = TkGCal${EXEEXT}

TCLKIT = $(top_builddir)/BuildData/tclkit${BEXEEXT}
BUILT_SOURCES = $(TCLKIT)


TkGCal${EXEEXT}: TkGCal.tcl $(wildcard Scripts/*.tcl)
	-rm -rf TkGCal.vfs TkGCal.kit
	$(TCLKIT) $(top_srcdir)/BuildScripts/sdx.kit qwrap $(srcdir)/TkGCal.tcl
	$(TCLKIT) $(top_srcdir)/BuildScripts/sdx.kit unwrap TkGCal.kit
	-rm -rf TkGCal.kit
	$(TCLKIT) $(top_srcdir)/BuildScripts/AddKitDir.kit TkGCal lib \
		$(SNITLIB)
	$(TCLKIT) $(top_srcdir)/BuildScripts/AddKitFile.kit TkGCal \
		lib/Common Scripts/*.tcl Scripts/*.gif Scripts/*.png \
		Scripts/*.xpm Scripts/*.xbm
	$(TCLKIT) $(top_srcdir)/BuildScripts/MakePkgIndex.kit TkGCal \
		Common
	$(TCLKIT) $(top_srcdir)/BuildScripts/sdx.kit wrap TkGCal${EXEEXT} \
		-runtime $(top_srcdir)/BuildData/$(TCLKITRUN)
	-rm -rf TkGCal.vfs TkGCal.kit 
	

$(top_builddir)/BuildData/tclkit${BEXEEXT}: FORCE
	$(MAKE) -C $(top_builddir)/BuildData tclkit${BEXEEXT}

FORCE:
