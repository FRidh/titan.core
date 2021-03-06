##############################################################################
# Copyright (c) 2000-2019 Ericsson Telecom AB
# All rights reserved. This program and the accompanying materials
# are made available under the terms of the Eclipse Public License v2.0
# which accompanies this distribution, and is available at
# https://www.eclipse.org/org/documents/epl-2.0/EPL-2.0.html
#
# Contributors:
#   Szabo, Bence Janos
#
##############################################################################
TOPDIR := ../../
include $(TOPDIR)/Makefile.regression

ifdef LCOV
COVERAGE_FLAG := -C
endif

# ${MAKEPROG} has the same content as the built-in ${MAKE},
# except the special handling of ${MAKE} does not apply.
# If we used ${MAKE} in the rules below, 'make -n' would succeed once,
# then fail on every subsequent invocation until a 'make clean' is done. 

MAKEPROG := ${MAKE}

all: GenerateMakefile GenerateMakefileFromTPD


GenerateMakefile:
	$(TTCN3_DIR)/bin/ttcn3_makefilegen -f $(MFGEN_FLAGS) $(COVERAGE_FLAG) -N -o MakefileN
	if [ `grep -c "\-N" ./MakefileN` -ne 1 ]; \
	then echo "Makefilegen generation with -N flag failed: Overall verdict: fail" && exit 1; fi

GenerateMakefileFromTPD:
	$(TTCN3_DIR)/bin/ttcn3_makefilegen -t UntaggedOnTopUnionSwitchTest.tpd -f $(MFGEN_FLAGS) $(COVERAGE_FLAG) -o MakefileN
	if [ `grep -c "\-N" ./binDefault/MakefileN` -ne 1 ]; \
	then echo "Makefilegen generation with -N flag failed: Overall verdict: fail" && exit 1; fi

clean:
	-rm -rf MakefileN binDefault

distclean: clean
	-rm -f *.out

.PHONY: all clean distclean GenerateMakefile GenerateMakefileFromTPD

