# AdditionalDocSpecs for Agent configuration

# DocSpecs — LaTeX White Book or article

## Objective
This specification describes how to reproduce the current documentation repository layout and build behavior for a White Book project or an article such as getting started

## Repository structure to reproduce
```text
/
├── MASTER.tex
├── getting_started.tex
├── .gitignore
├── Setup/
│   ├── Packages.tex
│   ├── Shortcuts.tex
│   └── Messages_pkg/
├── Backmatter/
├── Mainmatter/
├── Bibliography/
└── Figures/
```

### Structure rules
- `MASTER.tex` is the main book entry point.
- `getting_started.tex` is an article type.
- `Setup/Packages.tex` centralizes package imports and rendering configuration.
- `Setup/Shortcuts.tex` centralizes reusable LaTeX commands/macros.
- `Backmatter/`, `Mainmatter/`, and `Bibliography/` are included from entry points using `\include{...}` or `\input{...}`.
- `Figures/` stores image assets referenced by LaTeX sources.

## LaTeX style and conventions
- Document classes in use:
  - `book` for `MASTER.tex`
  - `article` for standalone documents (`HTAS_user_guide.tex`, `HTAS_FR.tex`)
- `MASTER.tex` language is configured through `Setup/Packages.tex` (`babel`, UTF-8, and T1 encoding). Standalone `.tex` files may define their own language setup.
- Shared typography/layout conventions are defined in `Setup/Packages.tex`:
  - `mathpazo`, `microtype`, `geometry`, `fancyhdr`, `fncychap`, `minitoc`, `listings`, `minted`.
- Shared semantic shortcuts are defined in `Setup/Shortcuts.tex` (for example `\hydrot`, `\cw`, `\cwv`, `\script{}`).
- Keep chapter/section hierarchy and formal white-book tone.

## Compiler and build requirements
- Use `pdflatex` as baseline compiler.
- Because `minted` is used in shared packages, compilation should support shell escape (`minted` calls the external Pygments process for syntax highlighting).

### Required commands
```bash
# Main white book
pdflatex -shell-escape -interaction=nonstopmode MASTER.tex
pdflatex -shell-escape -interaction=nonstopmode MASTER.tex

# Standalone guides
pdflatex -shell-escape -interaction=nonstopmode HTAS_user_guide.tex
pdflatex -shell-escape -interaction=nonstopmode HTAS_FR.tex
```

> Notes:
> - Run twice for references/table-of-contents stabilization.
> - If bibliography is enabled in `MASTER.tex`, run BibTeX in between LaTeX passes.

## Multiple `.tex` entry-point support
The project supports compiling multiple independent entry files:
- `MASTER.tex` (user_guide),
- `getting_started.tex` (standalone getting started <= 15 pages).

An agent reproducing this repository must keep these entry points independent and compilable separately.
