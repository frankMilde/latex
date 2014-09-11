# Main document
MAINFILE = the-zeitgeist-movement-defined_latex
 
# Which feature are to used in document
# index = Index/Stichwortverzeichnis
# abbr = Abkuerzungsverzeichnis
# bib = Literaturverzeichnis
#FEATURES = index abbr bib
FEATURES = bib

# Compiler for the LaTeX document
LATEX = pdflatex
LATEXFLAGS = -interaction=nonstopmode
 
# Program to create index
MAKEINDEX = makeindex
 
# Program to create bibliography
BIBTEX = bibtex
 
# Various shell commands
DEL = rm -f
ECHO = echo
VIEWPDF = evince
 
# Backups
BACKUPSUFFIX = ~
BACKUPFILES = $(patsubst %.tex,%.tex$(BACKUPSUFFIX),$(wildcard *.tex)) $(patsubst %.bib,%.bib$(BACKUPSUFFIX),$(wildcard *.bib))
 
.PHONY: help clean cleanaux cleanbackup cleanall cleanpdf showpdf
 
# Rules
all: $(MAINFILE).pdf
index: $(MAINFILE).ind $(MAINFILE).ilg
abbr: $(MAINFILE).nls
bib: $(MAINFILE).blg $(MAINFILE).bbl
 
# Display help
help:
	@$(ECHO) Rules
	@$(ECHO) ------
	@$(ECHO) all        : Create complete PDF with all features
	@$(ECHO) pdf        : Create PDF without features
	@$(ECHO) index      : Create index 
	@$(ECHO) abbr       : Create nomenclature/abbreviation
	@$(ECHO) bib        : Create bibliography
	@$(ECHO) clean      : Delete temporary files
	@$(ECHO) cleanbackup: Delete backup files
	@$(ECHO) cleanpdf   : Delete pdf file
	@$(ECHO) cleanall   : Execute clean, cleanbackup and cleanpdf
	@$(ECHO) showpdf    : Show PDF file
	@$(ECHO) 
	@$(ECHO) Infos 
	@$(ECHO) -----
	@$(ECHO) Main document: $(MAINFILE).tex
	@$(ECHO) Features     : $(FEATURES)
	@$(ECHO)
 
# PDF document
pdf: $(MAINFILE).tex
	@$(ECHO) ======================================================================
	@$(ECHO) PDF document
	@$(ECHO) ======================================================================
	$(LATEX) $(LATEXFLAGS) $(MAINFILE).tex
 
# Complete PDF document (Rule all)
$(MAINFILE).pdf: $(MAINFILE).tex $(FEATURES)
	@$(ECHO) ======================================================================
	@$(ECHO) Complete PDF document: 1. Run
	@$(ECHO) ======================================================================
	$(LATEX) $(LATEXFLAGS) $(MAINFILE).tex
 
	@$(ECHO) ======================================================================
	@$(ECHO) Complete PDF document: 2. Run
	@$(ECHO) ======================================================================
	$(LATEX) $(LATEXFLAGS) $(MAINFILE).tex
 
# Preparation
$(MAINFILE).idx $(MAINFILE).nlo $(MAINFILE).aux: $(MAINFILE).tex
	@$(ECHO) ======================================================================
	@$(ECHO) Preparation
	@$(ECHO) ======================================================================
	$(LATEX) $(LATEXFLAGS) $(MAINFILE).tex
 
# Index (Rule index)
$(MAINFILE).ind $(MAINFILE).ilg: $(MAINFILE).tex $(MAINFILE).idx
	@$(ECHO) ======================================================================
	@$(ECHO) Index
	@$(ECHO) ======================================================================
	$(MAKEINDEX) $(MAINFILE).idx
 
# Abbreviations (Rule abbr)
$(MAINFILE).nls: $(MAINFILE).tex $(MAINFILE).nlo
	@$(ECHO) ======================================================================
	@$(ECHO) Abbreviations
	@$(ECHO) ======================================================================
	$(MAKEINDEX) $(MAINFILE).nlo -s nomencl.ist -o $(MAINFILE).nls
 
# Bibliography (Rule bib)
$(MAINFILE).blg $(MAINFILE).bbl: $(MAINFILE).tex $(MAINFILE).bib $(MAINFILE).aux
	@$(ECHO) ======================================================================
	@$(ECHO) Bibliography
	@$(ECHO) ======================================================================
	$(BIBTEX) $(MAINFILE)
 
# Delete temporary files
clean:
	$(DEL) $(MAINFILE).aux
	$(DEL) $(MAINFILE).bbl
	$(DEL) $(MAINFILE).bit
	$(DEL) $(MAINFILE).blg
	$(DEL) $(MAINFILE).dvi
	$(DEL) $(MAINFILE).glo
	$(DEL) $(MAINFILE).idx
	$(DEL) $(MAINFILE).ilg
	$(DEL) $(MAINFILE).ilg
	$(DEL) $(MAINFILE).ind
	$(DEL) $(MAINFILE).lof
	$(DEL) $(MAINFILE).log
	$(DEL) $(MAINFILE).lot
	$(DEL) $(MAINFILE).nlo
	$(DEL) $(MAINFILE).nls
	$(DEL) $(MAINFILE).out
	$(DEL) $(MAINFILE).toc
 
# Delete aux files (of other tex sources as well)
cleanaux:
	$(DEL) *.aux
 
# Delete backup files
cleanbackup:
	$(DEL) $(BACKUPFILES)
 
# Delete pdf file
cleanpdf:
	$(DEL) $(MAINFILE).pdf
 
# Delete all temporary files in one sweep
cleanall: clean cleanaux #cleanbackup
 
# Show pdf file
showpdf: $(MAINFILE).pdf
	$(VIEWPDF) $(MAINFILE).pdf
