# MarkDocEditor Overview

MarkDocEditor is the official IDE for authoring structured Markdown documentation projects within the MarkDocSuite ecosystem.</br>
It provides a modern, cross-platform editing experience with integrated compilation, live preview, validation, asset management, and AI assistance.

---

## Purpose

MarkDocEditor enables writers, developers, and documentation teams to:

* Create and manage `.mdproj` and `.mbkproj` files
* Organize Markdown content into structured documentation
* Preview formatting and interactive elements in real time
* Compile output to `.mdg` (Markdown Group) and `.mbk` (Markdown Book) using MarkDocCompiler
* Extend the environment with plugins, templates, and integrated AI tools

---

## Project Types

### `.mdproj`

* Lightweight Markdown group project
* Compiles to `.mdg` — a self-contained, navigable document collection

### `.mbkproj`

* Book-style documentation project
* Compiles to `.mbk` — a structured, indexed package for full documentation delivery

---

## Key Features

* Rich text editing with Markdown syntax support
* Live preview via WebView2 with support for MathJax and Mermaid
* Drag-and-drop asset organization
* Document and project-wide validation
* Version control integration (Git)
* One-click build to `.mdg` or `.mbk` using embedded MarkDocCompiler
* Template and boilerplate management
* Plugin system for UI widgets, processors, and tools
* Context-aware AI assistance powered by MCP Protocol

---

## Integration

* **MarkDocCompiler**: Used as the underlying build engine
* **MarkDocViewer**: Used to preview `.mdg` and `.mbk` outputs
* **Plugin System**: Shared across all MarkDocSuite components

---

MarkDocEditor is the central tool for producing structured Markdown documentation with full lifecycle support—from authoring and editing to compiling and packaging.
