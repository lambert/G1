PROJNAME = G1_8051_ARDUONE_ZERO

LAYOUTS = \
	G1.001.00.01.01.pcb \
	G1.002.00.01.01.pcb

# Generic stuff follows from here.

notarget:
	@echo "Please specify a target:"
	@echo ""
	@echo "${MAKE} bom            Creates bom files"
	@echo "${MAKE} gerber         Creates Gerber files"
	@echo "${MAKE} eyecandy       Creates eyecandy files"
	@echo "${MAKE} ps             Creates ps plotfiles"
	@echo "${MAKE} test           Creates IPC-D-356 testfiles"
	@echo "${MAKE} all            Creates all of the above"

bom: $(LAYOUTS)
	for S in $(LAYOUTS); \
	do \
	pcb -x bom --xy-in-mm --bomfile $$S.bom $$S; \
	done;
	mv -u *.xy pnp/
	mv -u *.bom bom/

gerber: $(LAYOUTS)
	for S in $(LAYOUTS); \
	do \
	pcb -x gerber --name-style oshpark $$S; \
	done;
	mv -u *.fab fab/
	mv -u *.GBO fab/
	mv -u *.GBL fab/
	mv -u *.GBS fab/
#	mv -u *.gbp fab/
	mv -u *.GKO fab/
	mv -u *.GTO fab/
	mv -u *.GTL fab/
	mv -u *.gtp fab/
	mv -u *.GTS fab/
	mv -u *.TXT fab/
	mv -u *.XLN fab/
#	mv -u *.G?L fab/

eyecandy: $(LAYOUTS)
	for S in $(LAYOUTS); \
	do \
	pcb -x png --photo-mode --photo-mask-colour purple --photo-plating gold --only-visible --dpi 600 --outfile $$S.top.png $$S; \
	pcb -x png --photo-mode --photo-mask-colour purple --photo-plating gold --only-visible --dpi 600 --photo-flip-x --outfile $$S.bottom.png $$S; \
	done;
	mv -u *.png eyecandy/

ps: $(LAYOUTS)
	for S in $(LAYOUTS); \
	do \
	pcb -x ps --media A4 --align-marks --outline --drill-copper --drill-helper --show-legend --psfile $$S.ps $$S; \
	done;
	mv -u *.ps plotfiles/

test: $(LAYOUTS)
	for S in $(LAYOUTS); \
	do \
	pcb -x IPC-D-356 --netlistfile $$S.ipc-d-356 $$S; \
	done;
	mv -u *.ipc-d-356 test/

.DEFAULT_GOAL := notarget

all: bom gerber eyecandy ps test

# EOF #

