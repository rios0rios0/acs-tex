# Contributing

Contributions are welcome. By participating, you agree to maintain a respectful and constructive environment.

For coding standards, testing patterns, architecture guidelines, commit conventions, and all
development practices, refer to the **[Development Guide](https://github.com/rios0rios0/guide/wiki)**.

## Prerequisites

- [TeX Live](https://www.tug.org/texlive/) 2022+ (full or medium scheme) or [MiKTeX](https://miktex.org/download) 22.0+
- [Git](https://git-scm.com/downloads) 2.30+
- A LaTeX editor such as [TeXstudio](https://www.texstudio.org/), [VS Code](https://code.visualstudio.com/) with [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop), or [Overleaf](https://www.overleaf.com/)

## Development Workflow

1. Fork and clone the repository
2. Create a branch: `git checkout -b feat/my-change`
3. Navigate to the article directory:
   ```bash
   cd "Execução Especulativa - Limites da Exploração de Informações Sensíveis/article"
   ```
4. Compile the LaTeX document:
   ```bash
   pdflatex document.tex
   ```
5. Build the bibliography references:
   ```bash
   bibtex document
   ```
6. Run the full compilation cycle (required for correct references and citations):
   ```bash
   pdflatex document.tex
   bibtex document
   pdflatex document.tex
   pdflatex document.tex
   ```
7. Review the generated `document.pdf` for correctness
8. Commit following the [commit conventions](https://github.com/rios0rios0/guide/wiki/Life-Cycle/Git-Flow)
9. Open a pull request against `main`
