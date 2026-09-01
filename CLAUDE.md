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

Release workflow (`.github/workflows/release.yaml`) runs on push to `main` and delegates to `rios0rios0/pipelines`. Two Claude workflows delegate to the same shared pipelines: `claude-review.yaml` reviews pull requests and `claude-mention.yaml` answers `@claude` mentions; both authenticate with the `CLAUDE_CODE_OAUTH_TOKEN` secret. No LaTeX compilation in CI — correctness is verified manually.

## Commit and branching

Follow the [Development Guide](https://github.com/rios0rios0/guide/wiki) for commit conventions and branching strategy.

<!-- chlog:start -->
## Changelog (chlog) — MANDATORY

If the repository you are working in uses chlog (a `.chlog.yaml` or `.chlog.yml`
config file, or a `.changes/` directory, exists at the project root), the
following is binding and ALWAYS applies: whenever you make ANY change, you MUST
create a changelog fragment as part of the same change — automatically, without
being asked, before committing.

- Do NOT edit CHANGELOG.md directly; it is generated from fragments.
- Create the fragment with:
  `chlog new --kind <Kind> --body "<imperative description>"`
- Valid kinds: Added, Changed, Deprecated, Removed, Fixed, Security
- Choose the kind that best matches the change (e.g., new feature → Added,
  bug fix → Fixed, behavior change → Changed, removal → Removed, security fix → Security).
- If the change is backward-INCOMPATIBLE with the public API (a breaking
  change), you MUST add the `--breaking` flag:
  `chlog new --kind <Kind> --breaking --body "<description>"`.
  This is the ONLY thing that triggers a major version bump — the kind alone
  never does (per SemVer, major = incompatible change). When unsure whether a
  change breaks compatibility, ask the user instead of guessing.
- Fragments are YAML files in `.changes/unreleased/`; stage them with your commit.
- `chlog check` fails the build when a fragment is missing — never skip it.
<!-- chlog:end -->
