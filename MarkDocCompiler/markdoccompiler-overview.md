# MarkDocCompiler Overview

MarkDocCompiler is the build and packaging engine of the MarkDocSuite platform. It is responsible for transforming project-based Markdown content into distributable formats using a structured compilation process. MarkDocCompiler is used exclusively for programmatic or command-line builds and is intended to be integrated with authoring tools such as MarkDocEditor.

---

## Purpose

MarkDocCompiler enables reliable, repeatable builds of structured documentation projects. It consumes `.mdproj` and `.mbkproj` files and produces self-contained packages:

* `.mdproj` → `.mdg` (Markdown Group)
* `.mbkproj` → `.mbk` (Markdown Book)

It is not a user-facing tool. It has no UI and is not intended to preview or inspect content. Instead, it is invoked by the MarkDocEditor or CI tooling.

---

## Output Formats

### `.mdg` – Markdown Group

* Compiled from `.mdproj`
* Bundled static documents and assets
* Similar to a self-contained static site

### `.mbk` – Markdown Book

* Compiled from `.mbkproj`
* Feature-rich, searchable documentation package
* Comparable to `.chm` (Windows Help) format

---

## Usage

* MarkDocCompiler is triggered by MarkDocEditor, external build scripts, or potentially via a public API in the future
* It does not provide editing or preview capabilities
* All formatting, plugin, and packaging logic is handled in headless mode

---

## Responsibilities

* Parse and transform Markdown content using Markdig
* Apply AST-based plugin transformations
* Validate structure, links, and metadata
* Resolve and optimize media assets
* Package compiled outputs into `.mdg` or `.mbk` formats

---

This overview defines the core role of MarkDocCompiler in the MarkDocSuite ecosystem. Authoring, editing, UI, and file previews are provided separately by MarkDocEditor.
