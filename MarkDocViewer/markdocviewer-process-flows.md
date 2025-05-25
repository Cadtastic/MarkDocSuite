# MarkDocViewer Process and Sequence Flows

This document outlines the core interaction and rendering flows of the MarkDocViewer application. All diagrams reflect the current implementation using .NET MAUI, Markdig, WebView2, and the shared MarkDocSuite plugin system.

---

## 1. File Opening and Rendering Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as .NET MAUI UI
    participant Core as Core Engine
    participant FS as File System
    participant MP as Markdig Processor
    participant WebView as WebView2 Host

    User->>UI: Open .md / .mdg / .mbk file
    UI->>Core: Request render
    Core->>FS: Load file
    FS-->>Core: File content
    Core->>MP: Parse markdown
    MP-->>Core: AST
    Core->>WebView: Render HTML
    WebView-->>UI: Display preview
    UI-->>User: Show rendered document
```

---

## 2. Navigation and Search Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as .NET MAUI UI
    participant Core as Core Engine
    participant Index as Index Engine
    participant FS as File System

    User->>UI: Enter search query
    UI->>Core: Search request
    Core->>Index: Search AST index
    Index-->>Core: Match results
    Core->>UI: Show matches
    User->>UI: Select result
    UI->>Core: Navigate to section
    Core->>FS: Fetch file & section
    FS-->>Core: Document section
    Core->>UI: Scroll to match
```

---

## 3. Plugin Bootstrapping Flow

```mermaid
sequenceDiagram
    participant App as Application Startup
    participant Core as Core Engine
    participant PS as Plugin System
    participant Loader as Plugin Loader
    participant Plugin as Plugin

    App->>Core: Init
    Core->>PS: Load plugins
    PS->>Loader: Discover available
    loop Each plugin
        Loader->>Plugin: Load + verify
        Plugin-->>Loader: Capabilities
    end
    Loader-->>PS: Registered plugins
    PS-->>Core: Ready
```

---

## 4. Math and Diagram Injection Flow

```mermaid
sequenceDiagram
    participant Core as Core Engine
    participant AST as Markdown AST
    participant Injector as HTML Injector
    participant WebView as WebView2

    Core->>AST: Detect math/diagram blocks
    AST-->>Core: AST with extension tokens
    Core->>Injector: Convert AST to HTML
    Injector->>Injector: Inject MathJax / Mermaid
    Injector-->>Core: Renderable HTML
    Core->>WebView: Load content
```

---

## 5. Theme and Accessibility Update Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as .NET MAUI UI
    participant Core as Core Engine
    participant Settings as Settings Manager
    participant WebView as WebView2 Host

    User->>UI: Change theme or accessibility option
    UI->>Core: Notify update
    Core->>Settings: Apply new config
    Settings-->>Core: Settings saved
    Core->>WebView: Re-render with updated theme
    WebView-->>UI: New render
    UI-->>User: View updated preview
```

---

These flows represent the end-to-end behavior of the MarkDocViewer application for viewing, navigating, rendering, and customizing Markdown-based documentation.
