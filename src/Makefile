# This is a makefile that builds the Sepedi morphological parser
# *****************************************************************

# Remember the tabs in the beginning of the lines following the target
# line

# The first goal is to build nso.save
# This goal depends on nso.save and circum.fst being up to date

nso.fst: nso.save circum.fst
	@echo
	@echo "*** Building nso.fst ***" ;
	@echo
	@printf "read regex @\"../bin/nso.save\" .o. @\"../bin/circum.fst\" ; \n\
	save stack ../bin/nso.fst \n\
	quit \n" > /tmp/nso-fst-script
	@xfst < /tmp/nso-fst-script
	@rm -f /tmp/nso-fst-script

# The second goal il to build the circum.fst file
# This goal depends on circum.txt

circum.fst: circum.txt
	@echo
	@echo "*** Building circum.fst ***" ;
	@echo
	@printf "read regex < circum.txt \n\
	save stack ../bin/circum.fst \n\
	quit \n" > /tmp/circum-script
	@xfst < /tmp/circum-script
	@rm -f /tmp/circum-script

# The third goal is to build nso.save
# This goal depends on xfst-nso.bin and the lexicon file
# With more lexicon files, replace 1st line with
# printf "compile-source nso-lex.txt verb-nso-lex.txt \n\
# noun-nso-lex.txt adj-nso-lex.txt \n\

nso.save: nso-lex.txt xfst-nso.bin
	@echo
	@echo "*** Building nso.save ***" ;
	@echo
	printf "compile-source nso-lex.txt \n\
	read-rules ../bin/xfst-nso.bin \n\
	compose-result \n\
	save-result ../bin/nso.save \n\
	quit \n" > /tmp/nso-save-script
	@lexc < /tmp/nso-save-script
	rm -f /tmp/nso-save-script

# The fourth goal is to build xfst-nso.bin
# This goal depends on nso-rul.txt

xfst-nso.bin: xfst-nso.txt
	@echo
	@echo "*** Building xfst-nso.bin ***" ;
	@echo
	@printf "source < xfst-nso.txt \n\
	save ../bin/xfst-nso.bin \n\
	quit \n" > /tmp/nso-xfst-script
	@xfst < /tmp/nso-xfst-script
	@rm -f /tmp/nso-xfst-script

# Then, the intermediate files will be cleaned up
# Well, if we were to clean up

clean:
	@rm -f ../bin/*fst ../bin/*save ../bin/*bin

