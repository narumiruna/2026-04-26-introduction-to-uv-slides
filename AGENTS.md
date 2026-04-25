# Repository Guidelines

## Project Structure & Module Organization

This repository is a Marp slide deck. The primary deck lives in `README.md` and is rendered by GitHub Actions into `build/index.html`, `build/README.pdf`, and `build/README.pptx`. Supporting slide decks or reusable Markdown examples belong in `docs/`; `docs/template.md` is the current starter template. GitHub workflow configuration lives in `.github/workflows/marp-to-pages.yml`, with Marp authoring notes in `.github/marp.instructions.md`.

If local images are needed, place them under `img/`; the workflow copies that directory into `build/img` when it exists. Prefer stable local assets for important presentation visuals instead of expiring remote URLs.

## Build, Test, and Development Commands

- `docker run --rm -v "$PWD:/home/marp/app" -e MARP_USER=root:root marpteam/marp-cli:v3.0.2 README.md -o build/index.html` builds the main HTML deck locally.
- `docker run --rm -v "$PWD:/home/marp/app" -e MARP_USER=root:root marpteam/marp-cli:v3.0.2 README.md --allow-local-files -o build/README.pdf` builds the PDF export.
- `docker run --rm -v "$PWD:/home/marp/app" -e MARP_USER=root:root marpteam/marp-cli:v3.0.2 -I docs/ -o build/docs/` builds decks from `docs/`.

Create `build/` before local exports with `mkdir -p build`. The production workflow runs automatically on pushes to `main`; pull requests get a Pages preview.

## Coding Style & Naming Conventions

Write slides in Markdown with Marp front matter at the top, for example `marp: true`, `theme: gaia`, `paginate: true`, and optional `math: katex`. Separate slides with `---` on its own line. Keep slide headings short and use fenced code blocks with language tags such as `shell` when showing commands.

Use lowercase, hyphenated filenames for new decks and assets, for example `docs/uv-tools.md` or `img/install-flow.png`. Keep Markdown readable as plain text; avoid embedding generated HTML unless Marp requires it.

## Testing Guidelines

There is no separate automated test suite. Validate changes by rendering the affected deck locally and reviewing the output for broken images, clipped text, incorrect pagination, and code block readability. For workflow edits, check that the commands still match the Marp CLI image and output paths used in `.github/workflows/marp-to-pages.yml`.

## Commit & Pull Request Guidelines

Recent history uses short imperative commit messages such as `init commit`; keep commits concise and focused on one change. Pull requests should include a brief summary, note changed decks or assets, and attach screenshots or exported previews when visual layout changes are significant. Link related issues when available and mention any new external image or documentation source.

## Agent-Specific Instructions

Keep repository guidance scoped to this slide project. Do not add dependencies, build systems, or broad abstractions unless the deck workflow actually needs them.
