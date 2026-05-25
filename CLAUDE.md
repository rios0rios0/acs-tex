# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

ACSTeX is a LaTeX academic paper template using the IEEEtran document class for IEEE conference and journal submissions. The repo contains one example paper in Brazilian Portuguese.

## Build

No build system. Compile manually from inside an article directory:

```bash
cd "Execução Especulativa - Limites da Exploração de Informações Sensíveis/article"
pdflatex document.tex
bibtex document
pdflatex document.tex
pdflatex document.tex
```

The four-step cycle is required for correct bibliography and cross-references. A single `pdflatex` pass works for quick iteration when bibliography hasn't changed.

## Conventions

- Document class: `\documentclass[conference]{IEEEtran}`.
- Primary language: Brazilian Portuguese (`\selectlanguage{brazil}`); English loaded as secondary via `babel`.
- Source encoding: UTF-8 (`\usepackage[utf8]{inputenc}`).
- C code listings use the custom style at `listings/c/style.sty`.
- Each paper lives in its own top-level directory with an `article/` subdirectory containing the IEEEtran class/style files, `document.tex`, and `references.bib`.

## CI

Release workflow (`.github/workflows/release.yaml`) runs on push to `main` and delegates to `rios0rios0/pipelines`. No LaTeX compilation in CI — correctness is verified manually.

## Commit and branching

Follow the [Development Guide](https://github.com/rios0rios0/guide/wiki) for commit conventions and branching strategy.
