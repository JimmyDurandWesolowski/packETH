# packETHcli - ethernet packet generator
# By Miha Jemec <jemcek@gmail.com>
# Copyright 2014 Miha Jemec,

# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# as published by the Free Software Foundation; either version 3
# of the License, or (at your option) any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA  02111-1307, USA.

# Makefile for building packETHcli

ifeq ("$(origin D)", "command line")
  DEBUG = $(V)
endif
ifndef DEBUG
  DEBUG = 0
endif

SHELL = /bin/sh

INSTALL = /usr/bin/install -c
INSTALL_DATA = ${INSTALL} -m 644
PREFIX ?= /usr

CC := $(CROSS_COMPILE)$(CC)
LD := $(CROSS_COMPILE)$(LD)
CPPFLAGS =

LDFLAGS += -lm -lpthread
CFLAGS += -Wall -Wunused -Wmissing-prototypes
CFLAGS += -Wmissing-declarations -Werror -O3
ifdef SYSROOT
  CFLAGS += --sysroot=$(SYSROOT)
  LDFLAGS += --sysroot=$(SYSROOT)
endif

ifeq ($(DEBUG),1)
  CFLAGS += -g
endif # DEBUG


PROGRAM = packETHcli

all: $(PROGRAM)

$(PROGRAM): cli_send.o parse_snort_rules.o
	$(CC) $(CFLAGS) $(LDFLAGS) $^ -o $@

install: $(PROGRAM)
	$(INSTALL) $(PROGRAM) $(PREFIX)/bin/$(PROGRAM)
	if [ ! -d $(PREFIX)/share/pixmaps/$(PROGRAM) ]; then \
	  mkdir -p $(PREFIX)/share/pixmaps/$(PROGRAM); \
	fi
	$(INSTALL_DATA) pixmaps/* $(PREFIX)/share/pixmaps/$(PROGRAM)

test:
	$(CC) $(CFLAGS) $(LDFLAGS) -DTEST_SNORT_RULE_PARSING \
	  parse_snort_rules.c -o parse_snort_rules

clean:
	rm -f *.o *~ parse_snort_rules $(PROGRAM)
