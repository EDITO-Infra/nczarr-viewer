# NCZarr Viewer Documentation

This directory contains the documentation for the NCZarr Viewer project.

## Workflow

### 1. Pre-commit (Automatic)
- **Presentations are built automatically** when you commit markdown files
- Uses `make presentations` to build PDF and HTML presentations
- Ensures presentations are always up-to-date

### 2. Local Development
```bash
# Build presentations only
make presentations

# Build Sphinx HTML docs only  
make html

# Build everything
make all

# Clean build directory
make clean
```

### 3. GitHub Actions (CI/CD)
- **Sphinx HTML docs** are built in CI
- **Presentation files** are copied from pre-commit builds
- **Static files** (videos, etc.) are copied to build/html
- **GitHub Pages** deployment happens automatically

## File Structure

```
docs/
├── source/                 # Sphinx source files
│   ├── static/            # Static assets (videos, images)
│   └── *.rst              # ReStructuredText files
├── build/                  # Build output (generated)
│   └── html/              # Final HTML output
├── nczarr_viewer_presentation.md  # Marp presentation source
├── Makefile               # Build automation
├── requirements.txt       # Python dependencies
└── README.md             # This file
```

## Prerequisites

### For Presentations
```bash
# Install Marp CLI globally
npm install -g @marp-team/marp-cli
```

### For Sphinx Docs
```bash
# Install Python dependencies
pip install -r docs/requirements.txt
```

## Development

1. **Edit presentation**: Modify `nczarr_viewer_presentation.md`
2. **Pre-commit builds**: Presentations are built automatically
3. **Edit Sphinx docs**: Modify files in `source/`
4. **Test locally**: Run `make html` to preview
5. **Commit**: Pre-commit builds presentations, CI builds docs

## Troubleshooting

### Presentations not building
```bash
# Check if Marp is installed
marp --version

# Build manually
make presentations
```

### Sphinx docs not building
```bash
# Install dependencies
pip install -r docs/requirements.txt

# Clean and rebuild
make clean
make html
```
