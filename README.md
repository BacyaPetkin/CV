# Roman Dugaev — CV

[![Build CV](https://github.com/BacyaPetkin/CV/actions/workflows/main.yml/badge.svg)](https://github.com/BacyaPetkin/CV/actions/workflows/main.yml)

English and Russian CVs, built with XeLaTeX. Two pages each, with selectable text,
clickable contacts and a shared single-column layout inspired by the original
[Russell template](https://www.overleaf.com/latex/templates/russelresume/zqnypvvjsfvq).
The shared style uses system Noto Sans fonts, including Cyrillic.

## Build

On Debian/Ubuntu:

```sh
sudo apt-get update
sudo apt-get install --no-install-recommends \
  texlive-xetex texlive-latex-extra texlive-lang-cyrillic fonts-noto-core
./compile
```

On other systems, install XeLaTeX, the packages used in `cv.sty`, Russian language
support and Noto Sans. No Python, containers or separate CV generator is required.

```sh
./compile                    # both languages
./compile --language eng     # English only
./compile --language rus     # Russian only
./compile --help
```

PDFs are written to:

- `build/RomanDugaev_CV_eng.pdf`
- `build/RomanDugaev_CV_rus.pdf`

The script works from any current directory, runs XeLaTeX twice and stops on
errors. Intermediate files stay in `build/eng/` and `build/rus/`. Build output is
ignored by Git; remove `build/` for a clean rebuild.

## Edit

- `cv-eng.tex` — English content.
- `cv-rus.tex` — Russian content; keep factual changes aligned with English.
- `cv.sty` — shared typography, spacing, contact links and PDF metadata.

Both versions put current DEXOR projects on the first page and skills, earlier
work and education on the second. Rebuild both PDFs after editing and check page
breaks. Project descriptions are maintained manually from the source repositories
and supplied experience; building the CV does not require those repositories.

## Releases

Pushes and pull requests to `main`, plus manual Actions runs, build both PDFs and
save them in the `cv-pdfs` workflow artifact.

To publish downloadable CVs, create and **publish a GitHub release** with a tag
pointing to the desired revision (which must contain this workflow). The
[`release: published` event](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#release)
builds the tagged revision and attaches both named PDFs to that release.
This also applies to prereleases. A tag push or a draft release alone does not
publish PDFs.

The release job uses the built-in `GITHUB_TOKEN`; no additional secret is needed.
Re-running it replaces assets with the same names using
[`gh release upload --clobber`](https://cli.github.com/manual/gh_release_upload).
Only that job has permission to write release assets.
