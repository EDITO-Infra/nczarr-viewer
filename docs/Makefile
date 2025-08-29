# Minimal makefile for Sphinx documentation
#

# You can set these variables from the command line, and also
# from the environment for the first two.
SPHINXOPTS    ?=
SPHINXBUILD   ?= sphinx-build
SOURCEDIR     = source
BUILDDIR      = build
DOCS_DIR      = $(shell pwd)

# Put it first so that "make" without argument is like "make help".
help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

# Build Sphinx HTML documentation only
html:
	@$(SPHINXBUILD) -M html "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

# Build presentations (for pre-commit)
presentations:
	@echo "Building presentations $(DOCS_DIR)..."
	@marp $(DOCS_DIR)/nczarr_viewer_presentation.md --output nczarr_viewer_presentation.pdf --theme-set marp-pdf.css
	@marp $(DOCS_DIR)/nczarr_viewer_presentation.md --output html/nczarr_viewer_presentation.html --theme-set ../assets/marp.css
	@echo "Presentations built successfully!"

# Build everything (for manual builds)
all: html presentations

# Ensure build/html directory exists
$(BUILDDIR)/html:
	@mkdir -p $@

# Sphinx targets - route all unknown targets to Sphinx using the "make mode" option
# $(O) is meant as a shortcut for $(SPHINXOPTS).
.PHONY: help html presentations all clean

# Catch-all target for Sphinx (exclude our custom targets)
%:
	@if [ "$@" != "nczarr_viewer_presentation.md" ] && [ "$@" != "presentations" ] && [ "$@" != "all" ] && [ "$@" != "help" ] && [ "$@" != "html" ]; then \
		$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O); \
	fi

clean:
	rm -rf $(BUILDDIR)/*