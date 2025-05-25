# MarkDocSuite System Architecture

The MarkDocSuite platform is composed of three modular applications: MarkDocEditor, MarkDocCompiler, and MarkDocViewer. These components communicate through file-based integration and a shared plugin architecture.

---

## Architecture Overview

```mermaid
graph TB
    subgraph MarkDocSuite

      subgraph ProjectFiles["Project Files"]
         mdproj[.mdproj]
         mbkproj[.mbkproj]
      end

      subgraph MarkDocEditor
         Editor[MarkDocEditor]
      end

      subgraph MarkDocCompiler
         Compiler[MarkDocCompiler]
      end

      subgraph FileTypes["File Types"]
         mdg[.mdg]
         mbk[.mbk]
      end

      subgraph MarkDocViewer
         ViewerDesktop[MarkDocViewer - Desktop]
         ViewerShell[MarkDocViewer - Shell Extension]
         ViewerWeb[MarkDocViewer - Web Extension]
      end

      subgraph Shared
         Plugins[Plugin System]
         Assets[Markdown, Media, Metadata]
      end
    end

    %% Editor
    ProjectFiles --> MarkDocEditor

    %% Compiler
    ProjectFiles --> MarkDocCompiler
    MarkDocCompiler --> FileTypes

    %% Viewer
    mdg --> MarkDocViewer
    mbk --> MarkDocViewer

    %% Shared
    MarkDocEditor <--> Shared
    MarkDocCompiler <--> Shared
    MarkDocViewer <--> Shared

```

---

## Key Design Principles

* **Separation of Concerns**: Each application handles a distinct part of the documentation lifecycle: authoring, building, and viewing.
* **Interoperability via Files**: All components communicate using well-defined file formats (`.mdproj`, `.mbkproj`, `.mdg`, `.mbk`).
* **Shared Extensibility**: A unified plugin system allows plugins to be reused across Editor, Compiler, and Viewer.
* **Cross-Platform Delivery**: All components are built on .NET 8 and .NET MAUI to run on Windows/macOS.

---

This architecture ensures that MarkDocSuite can scale across user roles, workflows, and platforms while maintaining consistency, performance, and modularity.
