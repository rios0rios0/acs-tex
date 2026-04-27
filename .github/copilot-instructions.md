# Copilot Instructions for ACSTeX

## Project Overview

**ACSTeX** is a LaTeX academic paper template based on IEEE standards. It uses the official
**IEEEtran** document class for conference and journal submissions.

The repository contains a completed research paper titled *"Execução Especulativa: Limites da
Exploração de Informações Sensíveis"* (Speculative Execution: Limits of Exploiting Sensitive
Information), written in Brazilian Portuguese, which serves as a concrete usage example of the
template.

## Repository Structure

```
acs-tex/
├── .github/
│   └── copilot-instructions.md      # This file
├── Execução Especulativa - Limites da Exploração de Informações Sensíveis/
│   └── article/
│       ├── document.tex             # Main LaTeX source file
│       ├── references.bib           # BibTeX bibliography database
│       ├── IEEEtran.cls             # IEEE document class
│       ├── IEEEtran.bst             # IEEE bibliography style
│       ├── IEEEtranS.bst            # IEEE bibliography style (sorted variant)
│       └── listings/
│           ├── c/
│           │   └── style.sty        # Custom listings style for C code
│           ├── list01.c             # Spectre PoC code examples
│           └── ...                  # (list02.c through list06.c)
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

## Technology Stack and Dependencies

| Tool | Version | Purpose |
|------|---------|---------|
| TeX Live or MiKTeX | 2022+ / 22.0+ | LaTeX distribution |
| `pdflatex` | bundled | PDF generation engine |
| `bibtex` | bundled | Bibliography processing |
| IEEEtran | bundled | IEEE document class and styles |
| Git | 2.30+ | Version control |

### LaTeX Packages Used

- `cite` – citation handling
- `amsmath`, `amssymb`, `amsfonts` – mathematical typesetting
- `algorithmic`, `graphicx` – algorithms and figures
- `xcolor`, `listings` – syntax highlighting for code samples
- `babel` – bilingual support (Brazilian Portuguese + English)
- `hyperref` – hyperlinks and PDF metadata
- `textcomp`, `inputenc` – encoding and special characters

## Build Commands

There is no automated build system. Compile the LaTeX document manually from the article
directory.

### Navigate to the article directory

```bash
cd "Execução Especulativa - Limites da Exploração de Informações Sensíveis/article"
```

### Full compilation cycle (required for correct references and citations)

```bash
pdflatex document.tex   # Initial PDF pass
bibtex document         # Resolve bibliography
pdflatex document.tex   # Resolve cross-references
pdflatex document.tex   # Final stable PDF
```

Each `pdflatex` pass typically takes a few seconds. The output is `document.pdf`.

### Quick single-pass compile (no bibliography update)

```bash
pdflatex document.tex
```

## CI/CD Pipeline

There is no CI/CD pipeline configured for this repository. Validation is done manually by
inspecting the generated `document.pdf`.

## Development Workflow

1. Fork and clone the repository.
2. Create a feature branch: `git checkout -b feat/my-change`
3. Edit `document.tex` (or other LaTeX source files) in your preferred editor.
4. Run the full compilation cycle (see above) to produce `document.pdf`.
5. Review `document.pdf` for correctness (layout, references, code listings).
6. Commit following the [commit conventions](https://github.com/rios0rios0/guide/wiki/Life-Cycle/Git-Flow).
7. Open a pull request against `main`.

Refer to the [Development Guide](https://github.com/rios0rios0/guide/wiki) for commit message
conventions, branching strategy, and code review standards.

## Coding Conventions

- **Document class**: always use `\documentclass[conference]{IEEEtran}` for conference papers.
- **Language**: the primary language is Brazilian Portuguese (`\selectlanguage{brazil}`); English
  is loaded as a secondary language via `babel`.
- **Encoding**: source files use UTF-8 (`\usepackage[utf8]{inputenc}`).
- **Code listings**: C code samples live under `listings/` and use the custom style loaded with
  `\usepackage{listings/c/style}`. New code examples should follow the same pattern.
- **Section structure**: Introduction → Methodology → Results/Discussion → Conclusion →
  References (standard IEEE paper layout).
- **Citations**: use `\cite{}` for in-text citations and maintain `references.bib` in BibTeX
  format.

## Common Tasks

### Add a new code listing

1. Place the `.c` file in `listings/`.
2. Reference it in `document.tex` using:
   ```latex
   \lstinputlisting[language=C, style=c, caption={Caption text}, label={lst:labelname}]{listings/filenamehere.c}
   ```

### Add a new bibliography entry

1. Add the BibTeX entry to `references.bib`.
2. Cite it in the text with `\cite{EntryKey}`.
3. Re-run the full compilation cycle to resolve the new reference.

### Add a new paper (article)

1. Create a new top-level directory named after the paper title.
2. Copy the `IEEEtran.cls`, `IEEEtran.bst`, and `IEEEtranS.bst` class files into the new
   `article/` subdirectory.
3. Create `document.tex` and `references.bib` following the existing paper as a template.

## Troubleshooting

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| `?` or `[?]` in citations | `bibtex` not run or run before `pdflatex` | Run the full 4-step cycle |
| "Undefined control sequence" error | Missing `\usepackage` | Add the required package |
| Bibliography not updated | Stale `.aux`/`.bbl` files | Delete `document.aux`, `document.bbl`, `document.blg` and recompile |
| Encoding errors in PDF | Non-UTF-8 source file | Ensure editor saves files as UTF-8 |
| Missing `IEEEtran.cls` error | Class file not in article directory | Copy from another article directory |
