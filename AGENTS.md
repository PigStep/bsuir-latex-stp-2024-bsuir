# AGENTS.md - BSUIR LaTeX STP Template

## Overview

LaTeX thesis/project template conforming to BSUIR standards (СТП01-2024). Designed for course projects and diploma theses at BSUIR.

## Project Structure

```
├── main.tex              # Main document (entry point)
├── bsuir2025.sty         # Style file (218 lines)
├── intro.tex             # Introduction
├── conclusion.tex        # Conclusion
├── biblio.tex            # Bibliography setup
├── references.bib        # BibTeX entries
├── listings.inc.tex      # Code listings configuration
├── TitlePage.pdf         # Title page (Word → PDF)
├── TZ.pdf                # Technical specification
├── topic/                # Chapter files (part1-5.tex)
├── appendix/             # Appendices (prilA-E.tex, 91-schemPril.tex)
├── pic/                  # Images (PNG, JPG, PDF)
├── C/                    # C source code
├── AutoCad/              # CAD drawings (DWG, SVG)
└── fonts/                # Times New Roman (TTF)
```

## Build Commands

### Full Compilation (Local)

```bash
# XeLaTeX + Biber for bibliography (recommended)
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex

# PDFLaTeX (alternative)
pdflatex main.tex && biber main && pdflatex main.tex && pdflatex main.tex
```

### Incremental Compilation (Overleaf/Local)

```bash
# Test single chapter
xelatex '\include{topic/part1}\bye'

# Test bibliography only
xelatex main.tex && biber main
```

### Validation

```bash
# Check for undefined references
grep "LaTeX Warning: Reference" main.log

# Check for overfull hboxes
grep "Overfull" main.log

# Check compilation errors
grep "Error" main.log
```

## Code Style Guidelines

### File Organization

- **Entry point**: `main.tex` — orchestrates includes
- **Style**: `bsuir2025.sty` — all custom commands, packages, formatting
- **Content**: Separate `.tex` files per section
- **Never** use inline styling — always use custom commands

### Document Structure

```latex
% Numbered chapters
\chapter[ToC title]{Display title}
\section{Section Title}
\subsection{Subsection Title}

% Unnumbered (Introduction, Conclusion)
\unnumberedchapter{ВВЕДЕНИЕ}
\chapter*{ЗАКЛЮЧЕНИЕ}
```

### Paragraph Formatting

- Start paragraphs with `\hspace*{12.5 mm}`
- Indent: 1.25cm (set globally in `bsuir2025.sty`)
- Justified alignment

### Figure Commands

```latex
% Single figure
\insertfigure{label}{pic/image.png}{Caption text}{0.8\textwidth}

% Two figures
\insertfigurescustom{pic/img1.png}{pic/img2.png}{0.45\textwidth}
  {Combined caption}{label}{sidebyside}  % horizontal
\insertfigurescustom{pic/img1.png}{pic/img2.png}{0.8\textwidth}
  {Combined caption}{label}{stacked}     % vertical
```

### Table Format

```latex
\begin{table}[H]
  \caption{Table caption}
  \centering
  \begin{tabular}{...}
    ...
  \end{tabular}
\end{table}
```

### Code Listings

```latex
\lstset{
    basicstyle=\ttfamily\fontsize{12pt}{14pt}\selectfont,
    language=python,
    breaklines=true,
    xleftmargin=1em
}
```

### Label Naming

```latex
\label{fig:descriptive-name}   % Figures
\label{tab:descriptive-name}   % Tables
\label{sec:descriptive-name}   % Sections
\label{eq:descriptive-name}    % Equations
\label{pril:descriptive-name}  % Appendices
```

## LaTeX Packages (in bsuir2025.sty)

| Package | Purpose |
|---------|---------|
| `extsizes` | 14pt font support |
| `fontspec` + `fontenc` | Font management |
| `babel` (russian) | Cyrillic localization |
| `titlesec`/`titletoc` | Section/TOC formatting |
| `graphicx` | Images |
| `listings` + `listingsutf8` | Code listings |
| `geometry` | Page margins |
| `fancyhdr` | Headers/footers |
| `amsmath` | Math formulas |
| `caption` | Captions |
| `pdfpages` | PDF insertion |
| `enumitem` | Lists customization |

## Formatting Rules (СТП01-2024)

1. **Paper**: A4, margins (left: 30mm, right: 15mm, top/bottom: 20mm)
2. **Font**: Times New Roman, 14pt, single spacing
3. **Paragraph**: 1.25cm indent, justified
4. **Chapter headings**: Bold, uppercase, left-aligned with 12.5mm indent
5. **Section headings**: Bold, uppercase
6. **Subsection headings**: Bold, sentence case
7. **Lists**: Use `enumitem`, dash (–) for bullets
8. **Math**: Chapter-based numbering (2.1), "где" on new line

## Common Issues

| Problem | Solution |
|---------|----------|
| Overleaf timeout | Compile sections incrementally |
| Font warnings | Use `xelatex` for Cyrillic |
| Figure placement | Use `[H]` option |
| Encoding errors | Ensure UTF-8 everywhere |
| Missing references | Run xelatex-biber-xelatex-xelatex |

## Development Guidelines

### Before Making Changes

1. Read `STP_PROMPT.md` for exact formatting requirements
2. Review `bsuir2025.sty` for existing commands
3. Test with `main.tex` compilation

### Adding Features

1. Add custom commands to `bsuir2025.sty`
2. Document in this file
3. Test compilation
4. Verify against СТП01-2024

### Code Quality

- No magic numbers — use `\setlength` with named lengths
- Comment complex formatting decisions
- Keep `bsuir2025.sty` organized by section
- Use `\ProvidesPackage` with version date
