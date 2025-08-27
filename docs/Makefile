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

# Build Sphinx documentation
sphinx:
	$(SPHINXBUILD) -b html $(SOURCEDIR) $(BUILDDIR)/html

# Generate PDF presentation using Marp
pdf: nczarr_viewer_presentation.pdf

# Generate HTML presentation using Marp  
html: nczarr_viewer_presentation.html

# Generate PDF presentation using Marp
nczarr_viewer_presentation.pdf: nczarr_viewer_presentation.md
	marp --pdf $<

# Generate HTML presentation using Marp  
nczarr_viewer_presentation.html: nczarr_viewer_presentation.md
	marp --html $<

# Build all documentation
all: sphinx pdf html

# Clean all generated files
clean:
	rm -rf $(BUILDDIR)
	rm -f nczarr_viewer_presentation.pdf
	rm -f nczarr_viewer_presentation.html

# Install Marp CLI
install-marp:
	npm install -g @marp-team/marp-cli

# Check if Marp is installed
check-marp:
	@which marp || echo "Marp not found. Run 'make install-marp' to install."

.PHONY: help Makefile sphinx pdf html all clean install-marp check-marp