# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Sphinx-based documentation project** for training material on Credit Risk Policy Development in FinTech. The project is designed as a publicly available educational resource for newcomers to credit risk management, professionals refreshing their knowledge, and trainers teaching credit risk management.

The documentation is built using Sphinx with the Read the Docs theme and is hosted on Read the Docs platform.

## Building and Viewing Documentation

**Build HTML documentation:**
```bash
cd docs
make html
```

**Clean build artifacts:**
```bash
cd docs
make clean
```

**View built documentation:**
Open `docs/build/html/index.html` in a browser after building.

**Other output formats:**
- `make latexpdf` - Build PDF via LaTeX
- `make epub` - Build EPUB
- See `make help` for all available formats

## Documentation Structure

The documentation source lives in `docs/source/` and follows a hierarchical structure:

- **Entry point**: `docs/source/index.rst` - Main table of contents
- **Content format**: Mixed `.rst` (reStructuredText) and `.md` (Markdown) files
- **Section organization**: Each major section has a subdirectory with its own `index.rst`:
  - `fundamentals/` - Core concepts (decision making, bonds/interest rates, search algorithms)
  - `key_objective/` - Risk metrics and risk-reward objectives
  - `prediction/` - Forecasting, environment models, intervention response
  - `loan_origination/` - Antifraud and underwriting
  - `post_loan_management/` - Account management strategies (WIP)
  - `upstream_downstream/` - Broader ecosystem connections (WIP)
  - `practical_guides/` - Hands-on implementation guides

**Top-level documentation files** (in `docs/source/`):
- `product_structures.md` - Consumer finance product structures
- `data_role.md` - Role of data in credit risk
- `data_analysis.md` - General data analysis techniques
- `infrastructure.md` - Core infrastructure (WIP)
- `new_market.md` - Launching products in new markets (WIP)
- `unknowns.md` - Known unknowns in credit risk
- `resources.md` - Useful external resources
- `faq.md` - Common questions (WIP)

## Sphinx Configuration

**Configuration file**: `docs/source/conf.py`

**Key extensions enabled:**
- `myst_parser` - Markdown support with MyST extensions
- `sphinx.ext.mathjax` - Math equation rendering
- `sphinxcontrib.mermaid` - Mermaid diagram support
- `sphinx.ext.autodoc` - Python code documentation (though minimal Python code exists)
- `sphinx.ext.intersphinx` - Cross-referencing external docs

**Math support**:
- Uses MyST parser with `amsmath` and `dollarmath` extensions
- LaTeX math can be written inline with `$...$` or in blocks with `$$...$$`

**Theme**: `sphinx_rtd_theme` (Read the Docs theme) with navigation depth of 4 levels

## Content Authoring Guidelines

1. **File format**: Use `.md` (Markdown) for new content files - the project has migrated toward Markdown over reStructuredText
2. **Section indices**: Keep using `.rst` for `index.rst` files that define `toctree` structures
3. **Math notation**: Use LaTeX with dollar signs (enabled via MyST dollarmath)
4. **Diagrams**: Can include Mermaid diagrams using the `mermaid` directive
5. **Images**: Store images directly in `docs/source/` or relevant subdirectories (e.g., `visa.png`, `DiD.png`)
6. **WIP sections**: Some sections are marked as "WIP" (Work in Progress) in the main index - these contain placeholder content

## Dependencies

**Documentation dependencies** (in `docs/requirements.txt`):
- sphinx==7.1.2
- sphinx-rtd-theme==1.3.0rc1
- recommonmark
- myst-parser
- sphinxcontrib-mermaid

**Python build system**: Uses `flit_core` for package building (see `pyproject.toml`)

## Read the Docs Integration

**Configuration**: `.readthedocs.yaml`
- Build OS: Ubuntu 22.04
- Python version: 3.10
- Sphinx config: `docs/source/conf.py`
- Requirements: `docs/requirements.txt`

## Working with Content

When adding or modifying documentation:

1. **Adding a new standalone page**: Create `.md` file in `docs/source/` and add to the `toctree` in `docs/source/index.rst`
2. **Adding to an existing section**: Create `.md` file in the appropriate subdirectory and add to that section's `index.rst` toctree
3. **Creating a new section**: Create a subdirectory in `docs/source/`, add an `index.rst` with a toctree, then reference it from the main `index.rst`
4. **After changes**: Run `make html` from the `docs/` directory to rebuild and verify

## Note on Python Code

The repository contains a minimal Python package (`lumache.py`) that appears to be leftover from the Read the Docs tutorial template. The actual content is the Sphinx documentation, not the Python package.
