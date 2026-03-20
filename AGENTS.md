# AGENTS.md - BSUIR LaTeX STP Template

## Overview
This repository contains a LaTeX thesis/project template conforming to BSUIR standards (СТП01-2024). The goal is to modernize and generalize this template for wider use.

## Project Structure
```
├── bsuir2025.sty       # Main style file (200 lines)
├── shittt.tex          # Main document (88 lines)
├── title.tex           # Title page template
├── intro.tex           # Introduction
├── conclusion.tex      # Conclusion
├── biblio.tex          # Bibliography setup
├── references.bib      # BibTeX references
├── listings.inc.tex    # Code listings configuration
├── topic/              # Chapter files (part1-5.tex)
├── appendix/           # Appendix files (prilA-E.tex, 91-schemPril.tex)
├── pic/                # Images
├── C/                  # C source code
├── AutoCad/            # CAD drawings
└── TZ.pdf              # Technical specification
```

## Build Commands

### Local Compilation
```bash
# XeLaTeX (recommended for Cyrillic)
xelatex shittt.tex

# Or PDFLaTeX
pdflatex shittt.tex

# Full compilation with bibliography
xelatex shittt.tex && biber shittt && xelatex shittt.tex && xelatex shittt.tex
```

### Overleaf
- Upload as .zip with all .tex, .sty, images, and PDFs
- May need to compile sections incrementally due to time limits

## Code Style Guidelines

### LaTeX Conventions

#### File Organization
- Main document: `shittt.tex` (minimal, includes all parts)
- Style definitions: `bsuir2025.sty` (comprehensive package)
- Content: Separate `.tex` files per chapter/section
- No inline styling—use custom commands from `bsuir2025.sty`

#### Comments
```latex
%------------------------------------------------------------------------------
% Section separator with description
%------------------------------------------------------------------------------
```

#### Document Structure
```latex
\chapter{Chapter Title}      % Level 0 - numbered chapters
\section{Section Title}      % Level 1 - numbered sections  
\subsection{Subsection}     % Level 2 - subsections
\chapter*{Title}             % Unnumbered chapters (Introduction, Conclusion)
```

#### Custom Commands (use these)
```latex
\insertfigure{label}{path}{caption}{width}           % Single figure
\insertfigurescustom{path1}{path2}{width}{caption}{label}{mode}  % Two figures
```

Modes: `sidebyside` (horizontal), `stacked` (vertical)

#### Paragraph Indentation
- Always use `\hspace*{12.5 mm}` at start of paragraphs in sections
- Paragraph indent: 1.25cm (standard)

#### Figure/Table Captions
```latex
% Figures: Caption below, centered
\begin{figure}[H]
  \centering
  \includegraphics[width=0.8\textwidth]{path}
  \caption{Figure 1.1 – Description}
\end{figure}

% Tables: Caption above, left-aligned
\begin{table}[H]
  \caption{Table 1.1 – Description}
  \centering
  % table content
\end{table}
```

### Naming Conventions

#### Files
- Main `.tex` files: lowercase, descriptive (e.g., `intro.tex`, `conclusion.tex`)
- Chapter files: `partN.tex` in `topic/` directory
- Appendices: `prilX.tex` in `appendix/` directory
- Style file: `bsuirYYYY.sty` (year-based versioning)

#### Labels
```latex
\label{fig:descriptive-name}   % Figures
\label{tab:descriptive-name}   % Tables
\label{sec:descriptive-name}   % Sections
\label{eq:descriptive-name}    % Equations
```

#### Figures
- Store in `pic/` directory
- Formats: PNG, JPG, PDF (vector preferred)
- Filename: `descriptive_name.png`

### Package Usage

#### Required Packages (already in bsuir2025.sty)
- `extsizes` - 14pt font support
- `fontenc` (T2A) + `inputenc` (utf8) - Cyrillic
- `babel` (russianb) - Russian localization
- `titlesec` - Section formatting
- `titletoc` - TOC formatting
- `caption` - Captions
- `graphicx` - Images
- `listings` + `listingsutf8` - Code listings
- `geometry` - Page margins
- `fancyhdr` - Headers/footers
- `amsmath` - Math
- `pdfpages` - PDF insertion

#### Code Listings
```latex
\lstset{
    basicstyle=\ttfamily\fontsize{12pt}{12pt}\selectfont,
    language=python,
    breaklines=true,
    xleftmargin=1em
}
```

### Formatting Rules (СТП01-2024)

1. **Paper**: A4, margins (left: 30mm, right: 15mm, top/bottom: 20mm)
2. **Font**: Times New Roman, 14pt, single spacing
3. **Paragraph**: 1.25cm indent, justified alignment
4. **Headings**:
   - Chapters: Bold, uppercase, left-aligned with indent
   - Sections: Bold, uppercase
   - Subsections: Bold, sentence case
5. **Lists**: Use `enumitem` package, dash (–) for bullets
6. **Math**: Numbered by chapter (e.g., 2.1), "где" on new line

### Error Handling

#### Common Issues
1. **Overleaf timeout**: Compile sections incrementally
2. **Font warnings**: Use `xelatex` for Cyrillic
3. **Figure placement**: Use `[H]` for strict positioning
4. **Encoding issues**: Ensure UTF-8 throughout

#### Debugging
```bash
# View compilation log
latexlog shittt.log

# Check for undefined references
grep "LaTeX Warning: Reference" shittt.log
```

## Development Guidelines

### Before Making Changes
1. Read `STP_PROMPT.md` for exact formatting requirements
2. Review `bsuir2025.sty` for existing commands
3. Check `README.md` for usage examples

### Adding New Features
1. Add custom commands to `bsuir2025.sty`
2. Document new commands in this file
3. Test with `shittt.tex` compilation
4. Verify against СТП01-2024 requirements

### Code Quality
- No magic numbers—use `\setlength` with descriptive names
- Comment complex formatting decisions
- Keep `bsuir2025.sty` organized by section
- Use `\ProvidesPackage` with version date
