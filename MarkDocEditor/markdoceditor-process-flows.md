# MarkDocEditor Process and Sequence Flows

This document outlines the interactive and system-driven process flows for MarkDocEditor. These flows capture document editing, live preview, validation, compilation, and plugin operations within the application.

---

## 1. Markdown Editing and Live Preview

```mermaid
sequenceDiagram
    actor User
    participant UI as Editor UI
    participant AST as Markdown AST Engine
    participant Renderer as WebView2 Preview

    User->>UI: Edit Markdown (.md)
    UI->>AST: Parse content
    AST-->>UI: Updated AST
    UI->>Renderer: Render HTML
    Renderer-->>UI: Preview updated
    UI-->>User: Display live preview
```

---

## 2. Project Load and Navigation

```mermaid
sequenceDiagram
    actor User
    participant UI as Editor UI
    participant PM as Project Manager
    participant DM as Document Manager

    User->>UI: Open .mdproj or .mbkproj
    UI->>PM: Load project structure
    PM->>DM: Resolve document list and metadata
    DM-->>PM: Document graph
    PM-->>UI: Populate tree and project tabs
    UI-->>User: Show project interface
```

---

## 3. Validation Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as Editor UI
    participant Validator as Validation Engine
    participant Plugins as Plugin Loader

    User->>UI: Trigger validation
    UI->>Validator: Validate current file
    Validator->>Plugins: Run plugin validators
    Plugins-->>Validator: Rule results
    Validator-->>UI: Report issues
    UI-->>User: Display validation results
```

---

## 4. Compilation Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as Editor UI
    participant CI as Compiler Interface
    participant Compiler as MarkDocCompiler
    participant FS as File System

    User->>UI: Build project
    UI->>CI: Launch compilation
    CI->>Compiler: CLI call with .mdproj/.mbkproj
    Compiler->>FS: Parse & compile
    FS-->>Compiler: Build output
    Compiler-->>CI: Return success or errors
    CI->>UI: Display status
    UI-->>User: Show .mdg/.mbk or errors
```

---

## 5. AI Interaction Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as Editor UI
    participant AI as AI Integration
    participant MCP as MCP Protocol Client
    participant API as AI Service

    User->>UI: Select text + request AI help
    UI->>AI: Prepare context
    AI->>MCP: Format + route request
    MCP->>API: Call AI provider
    API-->>MCP: Return response
    MCP-->>AI: Extract result
    AI-->>UI: Update document
    UI-->>User: Show AI output
```

---

These flows define MarkDocEditor’s core functionality from project creation to build output, allowing for authoring, previewing, validating, and compiling within a single tool.
