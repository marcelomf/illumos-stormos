#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#
#
# Copyright (c) 2013 Andrew Stormont.  All rights reserved.
#
# Copyright 2006 Sun Microsystems, Inc.  All rights reserved.
# Use is subject to license terms.
#
#       Copyright (c) 1984, 1986, 1987, 1988, 1989 AT&T
#         All Rights Reserved
#

# cmd/msgfmt/Makefile

include ../Makefile.cmd

XOBJS=	xgettext.o

LXOBJS=	xgettext.lx.o

SOBJS=	msgfmt.o check_header.o

COBJS=	option.o util.o

BINPROG= msgfmt xgettext
PROG=  $(BINPROG)

YFLAGS += -d
LINTFLAGS +=	-um

POFILE= msgfmt_all.po
POFILES= $(SOBJS:%.o=%.po) $(COBJS:%.o=%.po)

ROOTBINPROG= $(BINPROG:%=$(ROOTBIN)/%)

CERRWARN += -_gcc=-Wno-parentheses
CERRWARN += -_gcc=-Wno-unused-label
CERRWARN += -_gcc=-Wno-uninitialized
CERRWARN += -_gcc=-Wno-unused-variable

.KEEP_STATE:

.PARALLEL:	$(SOBJS) $(COBJS) \
		$(XOBJS) $(LXOBJS)

all: $(PROG)

msgfmt:	$(SOBJS) $(COBJS)
	$(LINK.c) $(SOBJS) $(COBJS) -o $@ $(LDLIBS)
	$(POST_PROCESS)

xgettext: $(XOBJS) $(LXOBJS)
	$(LINK.c) $(XOBJS) $(LXOBJS) -o $@ $(LDLIBS)
	$(POST_PROCESS)

$(POFILE):	$(POFILES)
	$(RM) $@
	cat $(POFILES) > $@

install: all $(ROOTBINPROG)

clean:  
	$(RM) $(SOBJS) $(COBJS) \
		$(XOBJS) $(LXOBJS) \
		$(POFILE) $(POFILES) xgettext.lx.c

lint:
	$(LINT.c) $(SOBJS:%.o=%.c) $(COBJS:%.o=%.c) $(LDLIBS)
	$(LINT.c) $(XOBJS:%.o=%.c) $(LDLIBS)

include ../Makefile.targ
