# MarkDocEditor Technology Stack

MarkDocEditor is a cross-platform desktop application built on modern .NET technologies.</br>
It integrates rich authoring capabilities, live preview, project management, and direct communication with the MarkDocCompiler build engine.

---

## Platform

* **.NET 8 + .NET MAUI**
  Cross-platform UI framework for native desktop application delivery.

* **WebView2**
  Embedded Chromium renderer for live HTML preview and plugin-based rendering extensions.

---

## Languages and Frameworks

* **C#**
  Application logic, editor core, compiler interface, plugin system.

* **XAML**
  Used for declarative UI composition in .NET MAUI.

* **Markdig**
  AST-based Markdown processor with full support for GitHub Flavored Markdown, extensions, and pre-compilation transformations.

---

## Key Components

* **Live Preview Renderer**: Parses Markdown to HTML using Markdig + custom plugin extensions, rendered in WebView2.
* **Project System**: Supports `.mdproj` and `.mbkproj` creation, navigation, and file management.
* **Compiler Interface**: Shells out to the MarkDocCompiler executable or API for build operations.
* **Plugin Loader**: Dynamically loads C#-based UI and rendering extensions.
* **AI Integration**: Provides MCP-based AI service communication layer for contextual features.

---

## Build and Packaging

* **MSBuild + SDK-Style .csproj**
  Unified build pipeline for all platforms.

* **Single-Project MAUI Model**
  Consolidates resources and simplifies deployment.

* **WebView2 Runtime Management**
  Ensures embedded runtime or fallbacks for platform compatibility.

---

## File Type Integration

* **Project Files**:

  * `.mdproj` → compiles to `.mdg`
  * `.mbkproj` → compiles to `.mbk`

* **Viewable Files** (via preview tab or external viewer):

  * `.md`, `.mdg`, `.mbk`

---

This technology stack enables rapid authoring, flexible previewing, and seamless integration with the broader MarkDocSuite build ecosystem.
