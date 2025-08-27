# Minimal makefile for Sphinx documentation
#

# You can set these variables from the command line, and also
# from the environment for the first two.
SPHINXOPTS    ?=
SPHINXBUILD   ?= sphinx-build
SOURCEDIR     = source
BUILDDIR      = build

# Put it first so that "make" without argument is like "make help".
help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

# Build Sphinx HTML documentation
html:
	@$(SPHINXBUILD) -M html "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

# Build both docs and presentation
all: presentationhtml html

# Build PDF presentation
presentationpdf: nczarr_viewer_presentation.pdf

# Build HTML presentation
presentationhtml: $(BUILDDIR)/html
	marp nczarr_viewer_presentation.md --output $(BUILDDIR)/html/nczarr_viewer_presentation.html

# Ensure build/html directory exists
$(BUILDDIR)/html:
	@mkdir -p $@

# Rule to build PDF from markdown using pandoc
nczarr_viewer_presentation.pdf: nczarr_viewer_presentation.md
	marp $< --output $@

# Rule to build HTML from markdown using Marp in build/html directory (for direct use)
nczarr_viewer_presentation.html: nczarr_viewer_presentation.md
	marp $< --output $(BUILDDIR)/html/$@

# Sphinx targets - route all unknown targets to Sphinx using the "make mode" option
# $(O) is meant as a shortcut for $(SPHINXOPTS).
.PHONY: help html all presentationpdf presentationhtml clean

# Catch-all target for Sphinx (exclude our custom targets)
%:
	@if [ "$@" != "nczarr_viewer_presentation.md" ] && [ "$@" != "presentationhtml" ] && [ "$@" != "presentationpdf" ] && [ "$@" != "all" ] && [ "$@" != "help" ] && [ "$@" != "html" ]; then \
		$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O); \
	fi

clean:
	rm -rf $(BUILDDIR)/*
	rm -f nczarr_viewer_presentation.html
	rm -f nczarr_viewer_presentation.pdf