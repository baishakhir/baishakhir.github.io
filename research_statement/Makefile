# $Id: Makefile 1833 2006-06-19 21:51:36Z witchel $

.SUFFIXES: .fig .dvi .ps .pdf

VERSION = 0.0

#----------------------------------------------------------------------
# Source files.  Edit these variables for each new paper.
#----------------------------------------------------------------------

name = res

all: pdf

#----------------------------------------------------------------------
# LaTeX commands.
#----------------------------------------------------------------------

%.dvi:%.tex
	pdflatex $<

dvi: $(name).tex *.tex
	pdflatex $<

rub: $(name).tex 
	rubber -Wrefs -Wmisc $(name)

twice:
	pdflatex $(name)
	pdflatex $(name)

bib:
	bibtex $(name)
	pdflatex $(name)
	pdflatex $(name)


latex_junk = 	$(name).dvi \
		*.aux \
		*.log \
		$(name).blg \
		$(name).toc \
		psfig.aux \
		*.bbl \
		*.pdfsync

#----------------------------------------------------------------------
# Postscript/PDF generation.
#----------------------------------------------------------------------
crc:
	latex $(name).tex
	bibtex $(name)
	latex $(name).tex && latex $(name).tex
#	$(DVIPS) -P pdf -t letter -o $(name).ps $(name).dvi
	$(DVIPS) -o $(name).ps $(name).dvi
	ps2pdf -dSubsetFonts=true -dEmbedAllFonts=true -dCompatibilityLevel=1.4 -dPDFSETTINGS=/prepress -sPAPERSIZE=letter $(name).ps ray.pdf

$(name).ps:
ps: $(name).dvi *.tex
	latex $(name).tex && latex $(name).tex
#	$(DVIPS) -P pdf -t letter -o $(name).ps $(name).dvi
	$(DVIPS) -o $(name).ps $(name).dvi
	ps2pdf -dSubsetFonts=true -dEmbedAllFonts=true -dCompatibilityLevel=1.4 -dPDFSETTINGS=/prepress -sPAPERSIZE=letter $(name).ps ray.pdf

summary: summary.dvi

#DVIPS = dvips
DVIPS = dvips

%.ps:%.dvi
	$(DVIPS) -P pdf -t letter -o $@ $<

%.ps2:%.dvi
	$(DVIPS) -t letter -o ps2.tmp -p 2 $<
	mpage -2 -P ps2.tmp > $@
	rm ps2.tmp

pdf: 
	pdflatex $(name).tex

# DISTILL = distill
# DISTILL_FLAGS = -embedallfonts on -maxsubsetpct 100
# ps2pdf -dSubsetFonts=true -dEmbedAllFonts=true -dCompatibilityLevel=1.4 -dPDFSETTINGS=/prepress -sPAPERSIZE=letter mypaper.ps mypaper.pdf

DISTILL = ps2pdf
DISTILL_FLAGS =

%.pdf:%.ps
	$(DISTILL) $(DISTILL_FLAGS) $<

#----------------------------------------------------------------------
# Document previewers.
#----------------------------------------------------------------------

x:
	xdvi -s 5 $(name) &

gv: $(name).ps
	ghostview $(name).ps &


# Garbage files.
junk = $(latex_junk) *.ps *.pdf *.out


#----------------------------------------------------------------------
# Miscellaneous.
#----------------------------------------------------------------------

tags:
	etags $(latex_files)

clean:
	rm -f $(junk)

count:
	wc $(latex_files)
