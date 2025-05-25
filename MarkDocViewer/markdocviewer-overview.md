# MarkDocViewer Overview

MarkDocViewer is the viewing and inspection component of the MarkDocSuite platform. It enables users to open, preview, and interact with content packaged by MarkDocCompiler, including `.md`, `.mdg`, and `.mbk` formats. It is designed as a native, cross-platform application using .NET MAUI and WebView2 to deliver high-performance, extensible document rendering.

---

## Purpose

MarkDocViewer provides a dedicated, lightweight interface for reading and navigating documentation authored in Markdown. It supports project-aware viewing, sandboxed rendering of diagrams and math, and integration with search, annotations, plugins, and collaborative features.

---

## Key Capabilities

### Multi-Format Support

* Open and render `.md` files with styling and preview enhancements
* Load `.mdg` (Markdown Group) packages compiled from `.mdproj`
* Load `.mbk` (Markdown Book) packages compiled from `.mbkproj`

### Rendering Engine

* Uses Markdig for parsing Markdown into an AST
* Transforms AST into HTML with custom extensions
* Renders via WebView2 with injected support for:

  * **MathJax** (mathematical notation)
  * **Mermaid** (diagrams and flowcharts)

### Interface and Navigation

* Tabbed document viewer for working across multiple files
* Sidebar explorer for project and document hierarchy
* Anchored heading navigation, table of contents, and inline jump links
* Scroll/zoom and font scaling

### Desktop and Web Modes

* **Desktop**: .NET MAUI-based native Windows and macOS application
* **Web**: Runs in-browser via Blazor Hybrid (planned support)

### Performance and Accessibility

* Sandboxed WebView2 rendering ensures security
* Accessibility support for screen readers, keyboard navigation, and theming
* Fast startup, low resource usage, and smooth scrolling

---

## Integration with MarkDocSuite

MarkDocViewer integrates directly with:

* **MarkDocCompiler** output formats
* **Shared Plugin System** for adding custom render components
* **Search and Indexing** layer from project metadata
* **Windows Shell Extension** (used by Explorer previews)

---
