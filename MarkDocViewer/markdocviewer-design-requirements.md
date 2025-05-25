# MarkDocViewer Design Requirements

This document outlines the functional, non-functional, and technical requirements for the MarkDocViewer application. These specifications ensure compatibility with MarkDocSuite output, extensibility, performance, and user accessibility.

---

## 1. Functional Requirements

### 1.1 File Support

* The application shall open and render the following formats:

  * `.md` (single Markdown files)
  * `.mdg` (Markdown Group bundles)
  * `.mbk` (Markdown Book packages)

### 1.2 Rendering Pipeline

* The system shall parse Markdown using Markdig.
* The AST shall be transformed and rendered into HTML.
* The HTML shall be injected into a WebView2 sandbox.
* Optional scripts like MathJax and Mermaid shall be conditionally injected.

### 1.3 User Interface

* The UI shall be implemented using .NET MAUI.
* It shall support tabbed navigation between multiple documents.
* It shall provide a sidebar for navigating `.mdg` and `.mbk` structures.
* It shall allow users to zoom, scroll, and adjust themes.

### 1.4 Search and Indexing

* The application shall support full-text search across `.mdg` and `.mbk` documents.
* It shall generate a searchable index from parsed headings and metadata.

### 1.5 Plugin Support

* The application shall load plugins that implement shared interfaces.
* Supported plugin types:

  * Markdown AST transformers
  * Embedded content blocks
  * UI-side extensions (e.g., widgets, overlays)

---

## 2. Non-Functional Requirements

### 2.1 Performance

* Rendering time shall not exceed 200ms for standard-length documents.
* Indexing shall occur asynchronously without blocking the UI.

### 2.2 Portability

* The application shall run on Windows and macOS desktops.
* It shall support future extension to browser delivery via Blazor Hybrid.

### 2.3 Accessibility

* The system shall support screen reader navigation.
* It shall expose semantic content via ARIA tags in rendered output.

### 2.4 Security

* All rendered content shall be sandboxed within WebView2.
* Plugin execution shall occur in a constrained, verified environment.

---

## 3. Technical Constraints

### 3.1 Language and Framework

* **C#** for core logic and plugin integration
* **.NET 8 + .NET MAUI** for cross-platform UI
* **WebView2** for rendering HTML
* **Markdig** for Markdown parsing

### 3.2 Deployment and Build

* The system shall use MSBuild and .NET SDK-style projects.
* It shall bundle WebView2 and required runtime assets.
* All distributions shall be self-contained and require no external runtime.

---

These requirements define the core responsibilities of MarkDocViewer and ensure tight alignment with the broader MarkDocSuite ecosystem.
