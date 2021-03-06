MAIN = ellipses
MS=$(MAIN)
VERSION =
TGZFILE = $(MS)$(VERSION).tar.gz
ZIPFILE  = $(MS)${VERSION}.zip

# Stuff for making the archives
TEXDEPEND = texdepend
TAR = /bin/tar
ZIP = /usr/bin/zip

#  latex or  pdflatex?
LATEX = latex
# name of BibTeX command
BIBTEX = bibtex

# LaTeX flags
LATEXFLAGS = -interaction=nonstopmode


# texdepend, v0.96 (Michael Friendly (friendly@yorku.ca))
# commandline: texdepend ellipses.tex
INCLUDES = conjugate.tex linreg.tex simpson-iris.tex paradoxes.tex levdemo.tex measerror.tex avplot.tex MLM.tex criteria.tex kiss.tex discrim.tex ridge.tex ridge2.tex bayesian.tex mixed.tex hsbmix.tex conclusions.tex

#
PACKAGES = article.cls times.sty natbib.sty url.sty bm.sty graphicx.sty epigraph.sty comment.sty mdwlist.sty amsmath.sty amssymb.sty latexsym.sty color.sty afterpage.sty fancyhdr.sty
#
FIGS = fig/galton-corr.eps fig/inverse.eps fig/conjugate1.eps fig/conjugate2.eps fig/ellipse-geneig1.eps fig/ellipse-geneig2.eps fig/galton-reg3.eps fig/scatirisd1.eps fig/scatirisd3.eps fig/ellipses-demo.eps fig/vis-reg-prestige1.eps fig/vis-reg-prestige2.eps fig/contiris3.eps fig/between-within1.eps fig/between-within2.eps fig/between-HE1.eps fig/between-HE2.eps fig/levdemo21.eps fig/levdemo22.eps fig/vis-reg-coffee11.eps fig/vis-reg-coffee12a.eps fig/vis-reg-coffee12b.eps fig/vis-reg-coffee13.eps fig/coffee-stress1.eps fig/coffee-stress2.eps fig/coffee-avplot1.eps fig/coffee-avplot2.eps fig/heplot3a.eps fig/HE-contrasts-iris.eps fig/HE-can-iris.eps fig/kiss-demo.eps fig/kiss-demo2a.eps fig/kiss-demo2b.eps fig/ridge-demo.eps fig/ridge2.eps fig/hsbmix41.eps fig/hsbmix42.eps fig/hsbmix43.eps
#
BIB_FILES = ./references.bib
#
STYLES = /usr/share/texmf-texlive/tex/latex/psnfss/times.sty /usr/share/texmf-texlive/tex/latex/natbib/natbib.sty /usr/share/texmf-texlive/tex/latex/ltxmisc/url.sty /usr/share/texmf-texlive/tex/latex/tools/bm.sty /usr/share/texmf-texlive/tex/latex/graphics/graphicx.sty /usr/share/texmf-texlive/tex/latex/graphics/keyval.sty /usr/share/texmf-texlive/tex/latex/graphics/graphics.sty /usr/share/texmf-texlive/tex/latex/graphics/trig.sty /home/friendly/texmf/tex/latex/misc/epigraph.sty /usr/share/texmf-texlive/tex/latex/comment/comment.sty /usr/share/texmf-texlive/tex/latex/mdwtools/mdwlist.sty /usr/share/texmf-texlive/tex/latex/amsmath/amsmath.sty /usr/share/texmf-texlive/tex/latex/amsmath/amstext.sty /usr/share/texmf-texlive/tex/latex/amsmath/amsgen.sty /usr/share/texmf-texlive/tex/latex/amsmath/amsbsy.sty /usr/share/texmf-texlive/tex/latex/amsmath/amsopn.sty /usr/share/texmf-texlive/tex/latex/amsfonts/amssymb.sty /usr/share/texmf-texlive/tex/latex/amsfonts/amsfonts.sty /usr/share/texmf-texlive/tex/latex/base/latexsym.sty /usr/share/texmf-texlive/tex/latex/graphics/color.sty /usr/share/texmf-texlive/tex/latex/tools/afterpage.sty /usr/share/texmf-texlive/tex/latex/fancyhdr/fancyhdr.sty

ALTFIGS =
#

SHIPSTYLES = 

EXTRAS = $(MAIN:%=%.aux) $(MAIN:%=%.bbl)  \
 $(SHIPSTYLES) Makefile 

ALLFILES = $(MAIN).tex $(MAIN).pdf  $(INCLUDES) $(BIB_FILES) $(FIGS) $(ALTFIGS) $(EXTRAS)

# Dependencies
#
paper:	$(MAIN).tex $(INCLUDES)
	$(LATEX) $(LATEXFLAGS) $(MAIN).tex
	-@egrep -c 'Citation .* undefined.' $(MAIN).log && ($(BIBTEX) $(MAIN);$(LATEX) $(MAIN))
	dvipdf $(MAIN)

${ZIPFILE}: ${ALLFILES}

${TARFILE}: ${ALLFILES}

$(MAIN).dvi: $(MAIN).tex $(FIGS)

$(MAIN).ps: $(MAIN).dvi


## Hand edited FIGLIST because of multiple images/fig
#FIGLIST:
#	$(TEXDEPEND) -format=1 -print=f $(MAIN)  | perl -pe 'unless (/^#/){$f++; s/^/Figure $f: /}' > FIGLIST
	


# Targets for archives
# note
zip: ${ALLFILES}
	$(ZIP) -r -u  $(ZIPFILE) $(ALLFILES)

tar: ${ALLFILES}
	$(TAR) cvhf - $(ALLFILES) | $(GZIP) > $(TGZFILE) 

git-push: ${ALLFILES}
	git push -u origin master
