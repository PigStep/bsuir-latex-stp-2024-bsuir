# AGENTS.md - BSUIR LaTeX STP Template

## Overview

LaTeX thesis/project template conforming to BSUIR standards (СТП01-2024). Designed for course projects and diploma theses at BSUIR. This is a document project, not software - there are no traditional tests or linting.

## Project Structure

```
├── main.tex              # Main document (entry point)
├── bsuir2025.sty         # Style file (254 lines) - ALL custom commands here
├── intro.tex             # Introduction (unnumbered)
├── conclusion.tex        # Conclusion (unnumbered)
├── biblio.tex            # Bibliography setup
├── references.bib        # BibTeX entries
├── listings.inc.tex      # Code listings configuration
├── TitlePage.pdf         # Title page (Word → PDF)
├── TZ.pdf                # Technical specification (PDF)
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
# XeLaTeX + Biber for bibliography (RECOMMENDED)
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex

# Alternative: PDFLaTeX
pdflatex main.tex && biber main && pdflatex main.tex && pdflatex main.tex

# Quick script (save as compile.sh)
#!/bin/bash
xelatex main.tex && biber main && xelatex main.tex && xelatex main.tex
```

### Testing Single Chapter

```bash
# Compile only one chapter (fast feedback)
xelatex '\include{topic/part1}\bye'

# Test a specific included file with preamble
xelatex '\documentclass[a4paper,14pt]{extreport}\usepackage{bsuir2025}\begin{document}\include{topic/part1}\end{document}'
```

### Overleaf/Cloud Compilation

Since Overleaf has timeout limits, compile incrementally:
- First run: `xelatex main.tex` (generates ToC, page refs)
- Second run: `biber main` (bibliography)
- Third run: `xelatex main.tex` (final)

### Validation Commands

```bash
# Check for undefined references
grep "LaTeX Warning: Reference" main.log

# Check for undefined citations
grep "Citation.*undefined" main.log

# Check for overfull hboxes (text overflow)
grep "Overfull" main.log

# Check for underfull hboxes
grep "Underfull" main.log

# Check compilation errors
grep "Error" main.log

# Check all warnings
grep "Warning" main.log
```

### Debugging

```bash
# Interactive error mode - stops at first error
xelatex -interaction=nonstopmode main.tex

# View .log file for detailed errors
cat main.log | head -100
```

## Code Style Guidelines

### File Organization (CRITICAL)

- **Entry point**: `main.tex` — orchestrates all includes via `\include{...}`
- **Style file**: `bsuir2025.sty` — ALL custom commands, packages, and formatting MUST go here
- **Content files**: Separate `.tex` files per section (intro, conclusion, each chapter)
- **NEVER use inline styling** — always use custom commands from `bsuir2025.sty`

### Document Structure

```latex
% Numbered chapters (use for main content)
\chapter[ToC title]{Display title}
\section{Section Title}
\subsection{Subsection Title}
\subsection*{Subsection without number}  % Rarely used

% Unnumbered chapters (Introduction, Conclusion only)
\unnumberedchapter{ВВЕДЕНИЕ}
\chapter*{ЗАКЛЮЧЕНИЕ}
```

### Paragraph Formatting

- Paragraphs: Start with `\hspace*{12.5 mm}` before first line (already set globally)
- Indent: 1.25cm (configured in `bsuir2025.sty` via `\setlength{\parindent}{1.25cm}`)
- Alignment: Justified (default)
- Spacing: Single-spaced, no additional vertical space between paragraphs

### Figure Commands

```latex
% Single figure
\insertfigure{label}{pic/image.png}{Caption text}{0.8\textwidth}

% Two figures - horizontal layout
\insertfigurescustom{pic/img1.png}{pic/img2.png}{0.45\textwidth}
  {Combined caption}{label}{sidebyside}

% Two figures - vertical layout
\insertfigurescustom{pic/img1.png}{pic/img2.png}{0.8\textwidth}
  {Combined caption}{label}{stacked}

% Reference in text: \ref{fig:label}
```

### Table Format

```latex
\begin{table}[H]
  \caption{Table caption}
  \centering
  \begin{tabular}{|c|p{8cm}|c|}
    \hline
    Header & Header & Header \\
    \hline
    data & data & data \\
    \hline
  \end{tabular}
  \label{tab:descriptive-name}
\end{table}
```

### Code Listings

```latex
% Configure globally in bsuir2025.sty or per-listing
\lstset{
    basicstyle=\ttfamily\fontsize{12pt}{14pt}\selectfont,
    language=C,
    breaklines=true,
    xleftmargin=1em,
    numbers=left
}

% In document
\begin{lstlisting}[label=code:example, caption=C code example]
int main() {
    return 0;
}
\end{lstlisting}
```

### Label Naming Conventions

```latex
\label{fig:descriptive-name}   % Figures
\label{tab:descriptive-name}   % Tables
\label{sec:descriptive-name}   % Sections
\label{eq:descriptive-name}    % Equations
\label{pril:descriptive-name}  % Appendices
\label{code:descriptive-name}  % Code listings
```

### Bibliography

```latex
% In references.bib
@article{key2024,
  author = {Author Name},
  title = {Title},
  journal = {Journal},
  year = {2024}
}

% In biblio.tex
\printbibliography[heading=bibintoc]
```

## LaTeX Packages (in bsuir2025.sty)

| Package | Purpose |
|---------|---------|
| `extsizes` | 14pt font support |
| `fontspec` + `fontenc` | Font management (XeLaTeX) |
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
| `microtype` | Typography improvements |
| `tocloft` | TOC customization |

## Formatting Rules (СТП01-2024)

1. **Paper**: A4, margins (left: 30mm, right: 15mm, top/bottom: 20mm)
2. **Font**: Times New Roman, 14pt, single spacing
3. **Paragraph**: 1.25cm indent, justified alignment
4. **Chapter headings**: Bold, uppercase, left-aligned with 12.5mm indent
5. **Section headings**: Bold, uppercase
6. **Subsection headings**: Bold, sentence case
7. **Lists**: Use `enumitem`, dash (–) for bullets
8. **Math**: Chapter-based numbering (2.1), "где" on new line
9. **Captions**: "Рисунок X.Y - caption" format
10. **Tables**: "Таблица X.Y - caption" format

## Common Issues & Solutions

| Problem | Solution |
|---------|----------|
| Overleaf timeout | Compile incrementally, test single chapters |
| Font warnings | Use `xelatex` for Cyrillic support |
| Figure placement | Use `[H]` option (force here) |
| Encoding errors | Ensure UTF-8 everywhere (file encoding) |
| Missing references | Run full xelatex-biber-xelatex-xelatex cycle |
| Overfull hbox | Adjust text or use `\LineBreak` |
| Table too wide | Use `tabularx` or reduce column widths |

## Development Workflow

### Before Making Changes

1. Review `bsuir2025.sty` for existing custom commands
2. Check `main.tex` for document structure
3. Test compilation with `xelatex main.tex`

### Adding New Features

1. Add custom commands to `bsuir2025.sty`
2. Document the command in AGENTS.md
3. Test compilation
4. Verify against СТП01-2024 formatting requirements

### Code Quality Principles

- No magic numbers — use `\setlength` with named lengths
- Keep `bsuir2025.sty` organized by section (packages, geometry, headings, commands)
- Use `\ProvidesPackage` with version date
- All Russian text must be in UTF-8

## Quick Reference

```bash
# Full build
xelatex main.tex && biber main && xelatex main.tex && xelatex main.tex

# Check for errors
grep -i "error" main.log

# Check references
grep "Reference" main.log
```