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
	@echo "Copying static files to build/html/static..."
	@cp -r $(DOCS_DIR)/source/static $(BUILDDIR)/html/static
	@echo "✅ Static files copied to build/html/static"

# Build presentations (for local use)
presentations:
	@echo "Building presentations locally..."
	@marp $(SOURCEDIR)/nczarr_viewer_presentation.md --output $(SOURCEDIR)/nczarr_viewer_presentation.pdf --theme $(SOURCEDIR)/static/styles/edito-marp.css --allow-local-files
	@marp $(SOURCEDIR)/nczarr_viewer_presentation.md --output $(SOURCEDIR)/nczarr_viewer_presentation.html --theme $(SOURCEDIR)/static/styles/edito-marp.css --allow-local-files
	@echo "✅ Local presentations built successfully!"

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
	rm -rf $(DOCS_DIR)/nczarr_viewer_presentation.pdf
	rm -rf $(SOURCEDIR)/nczarr_viewer_presentation.html