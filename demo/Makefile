# Copyright (c) 2012 The Chromium Authors. All rights reserved.
# Use of this source code is governed by a BSD-style license that can be
# found in the LICENSE file.

#
# GNU Make based build file.  For details on GNU Make see:
#   http://www.gnu.org/software/make/manual/make.html
#

PROJECTS:= \
  pi_generator \
  life \
  drive \
  flock \
  nacl_io \
  earth \
  voronoi \

HTTPD:=../../tools/httpd.py

ifeq ($(TOOLCHAIN),all)
TOOLCHAIN_ARG:=TOOLCHAIN=all
endif

# Define the default target
all:

#
# Target Macro
#
# Macro defines a phony target for each example, and adds it to a list of
# targets.
#
# Note: We use targets for each project (instead of an explicit recipe) so
# each project can be built in parallel.
#
define TARGET
ALL_TARGET_LIST+=$(1)_ALL_TARGET
.PHONY: $(1)_ALL_TARGET
$(1)_ALL_TARGET:
	+$(MAKE) -C $(1) $(TOOLCHAIN_ARG) all

CLEAN_TARGET_LIST+=$(1)_CLEAN_TARGET
.PHONY: $(1)_CLEAN_TARGET
$(1)_CLEAN_TARGET:
	+$(MAKE) -C $(1) $(TOOLCHAIN_ARG) clean
endef


# Define the various targets via the Macro
$(foreach proj,$(PROJECTS),$(eval $(call TARGET,$(proj))))

.PHONY: all
all: $(ALL_TARGET_LIST)
	@echo Done building targets.

.PHONY: clean
clean: $(CLEAN_TARGET_LIST)
	@echo Done cleaning targets.

.PHONY: run
run: all
	@echo Starting up python webserver.
	python $(HTTPD)

# Phony aliases for backward compatibility
RUN: run

all_versions:
	+$(MAKE) TOOLCHAIN=all

.PHONY: RUN all_versions
