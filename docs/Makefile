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

# Check if marp is installed, install if not
check-marp:
	@if ! command -v marp >/dev/null 2>&1; then \
		echo "❌ marp-cli not found. Installing..."; \
		if command -v npm >/dev/null 2>&1; then \
			npm install -g @marp-team/marp-cli; \
		elif command -v brew >/dev/null 2>&1; then \
			brew install marp-cli; \
		elif command -v apt-get >/dev/null 2>&1; then \
			echo "Please install marp-cli manually: npm install -g @marp-team/marp-cli"; \
			exit 1; \
		else \
			echo "Please install marp-cli manually: npm install -g @marp-team/marp-cli"; \
			exit 1; \
		fi; \
	else \
		echo "✅ marp-cli is available"; \
	fi

# Build presentations (for local use)
presentations: check-marp
	@echo "Building presentations locally..."
	@marp $(SOURCEDIR)/nczarr_viewer_presentation.md --output $(DOCS_DIR)/nczarr_viewer_presentation.pdf --theme $(SOURCEDIR)/static/styles/edito-marp.css --allow-local-files
	@marp $(SOURCEDIR)/nczarr_viewer_presentation.md --output $(SOURCEDIR)/nczarr_viewer_presentation.html --theme $(SOURCEDIR)/static/styles/edito-marp.css --allow-local-files
	@echo "✅ Local presentations built successfully!"

# Build everything (for manual builds)
all: html presentations

# Ensure build/html directory exists
$(BUILDDIR)/html:
	@mkdir -p $@

# Sphinx targets - route all unknown targets to Sphinx using the "make mode" option
# $(O) is meant as a shortcut for $(SPHINXOPTS).
.PHONY: help html presentations check-marp all clean

# Catch-all target for Sphinx (exclude our custom targets)
%:
	@if [ "$@" != "nczarr_viewer_presentation.md" ] && [ "$@" != "presentations" ] && [ "$@" != "all" ] && [ "$@" != "help" ] && [ "$@" != "html" ]; then \
		$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O); \
	fi

clean:
	rm -rf $(BUILDDIR)/*
	rm -rf $(DOCS_DIR)/nczarr_viewer_presentation.pdf
	rm -rf $(SOURCEDIR)/nczarr_viewer_presentation.html