# MarkDocViewer Technology Stack

This document describes the core technologies used to implement MarkDocViewer. The system is built using a modern .NET-native stack designed for speed, cross-platform support, and compatibility with MarkDocCompiler output formats.

---

## Platform

* **.NET 8 + .NET MAUI**
  Cross-platform UI framework for building native Windows and macOS desktop applications.

* **Blazor Hybrid (Planned)**
  Enables future web-based access via WebAssembly and .NET MAUI integration.

---

## Languages

* **C#**
  Primary language for all application logic, UI binding, data flow, and plugin integration.

* **XAML**
  Used for defining native UI layout and styling within .NET MAUI.

---

## Rendering Engine

* **Markdig**
  AST-based Markdown parser with support for GitHub Flavored Markdown (GFM).

  * Custom extensions for code blocks, math, diagrams, and more.

* **WebView2**
  Embedded Chromium engine used for rendering HTML content:

  * Injects MathJax for LaTeX-style mathematical notation
  * Injects Mermaid for diagrams and flowcharts
  * Supports local or sandboxed rendering mode

---

## Supported File Formats

* `.md` — Standard Markdown
* `.mdg` — Markdown Group (bundled collection of markdown files)
* `.mbk` — Markdown Book (packaged documentation similar to .chm)

These formats are compiled by MarkDocCompiler and rendered natively by MarkDocViewer.

---

## Build and Packaging

* **MSBuild + .NET SDK**
  Used to build and package self-contained desktop apps for each platform.

* **Single Project MAUI Model**
  Centralizes resources and simplifies platform targeting.

* **WebView2 Runtime Packaging**
  Bundled as part of Windows deployment or resolved on-demand.

---

## Extensibility and Plugins

* MarkDocViewer shares the same plugin system as MarkDocCompiler
* Plugins are written in C# and conform to shared interfaces
* Supported plugin types include:

  * Render pipeline transformers
  * Sidebar widgets
  * Script injectors (MathJax, Mermaid)

---

This technology stack enables consistent rendering and behavior across all components of the MarkDocSuite ecosystem.
