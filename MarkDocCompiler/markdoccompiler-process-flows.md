# MarkDocCompiler Process and Sequence Flows

This document outlines the core execution flows for the MarkDocCompiler system. These flows represent internal logic only and do not include UI interactions. All sequences are applicable in both CLI and programmatic invocation contexts.

---

## 1. Compilation from `.mdproj` to `.mdg`

```mermaid
sequenceDiagram
    participant CLI as CLI or MarkDocEditor
    participant Compiler as Core Engine
    participant Loader as Project Loader
    participant Validator as Validation Engine
    participant Processor as Markdown Processor
    participant Plugins as Plugin System
    participant Assets as Asset Manager
    participant Packager as Package Generator

    CLI->>Compiler: Start `.mdproj` compilation
    Compiler->>Loader: Parse project file
    Loader-->>Compiler: Project structure
    Compiler->>Validator: Run validation rules
    Validator-->>Compiler: Validation results
    Compiler->>Plugins: Run AST transformers
    Plugins-->>Compiler: Modified AST
    Compiler->>Processor: Compile markdown
    Processor-->>Compiler: Render tree
    Compiler->>Assets: Optimize and embed media
    Assets-->>Compiler: Resolved asset map
    Compiler->>Packager: Create `.mdg` package
    Packager-->>Compiler: Output complete
    Compiler-->>CLI: Build successful
```

---

## 2. Compilation from `.mbkproj` to `.mbk`

```mermaid
sequenceDiagram
    participant CLI as CLI or MarkDocEditor
    participant Compiler as Core Engine
    participant Loader as Project Loader
    participant Validator as Validation Engine
    participant Processor as Markdown Processor
    participant Plugins as Plugin System
    participant Assets as Asset Manager
    participant Packager as Package Generator

    CLI->>Compiler: Start `.mbkproj` compilation
    Compiler->>Loader: Parse book structure
    Loader-->>Compiler: Project definition
    Compiler->>Validator: Enforce schema and structure
    Validator-->>Compiler: Pass/fail result
    Compiler->>Plugins: Execute content transforms
    Plugins-->>Compiler: Final AST
    Compiler->>Processor: Convert markdown to HTML
    Processor-->>Compiler: HTML blocks
    Compiler->>Assets: Resolve linked assets
    Assets-->>Compiler: Embedded resources
    Compiler->>Packager: Build `.mbk` container
    Packager-->>Compiler: Success output
    Compiler-->>CLI: Book build completed
```

---

## 3. Plugin Load and Validation Flow

```mermaid
sequenceDiagram
    participant Compiler as Core Engine
    participant Plugins as Plugin System
    participant Loader as Plugin Loader
    participant Plugin as Plugin Entry

    Compiler->>Plugins: Initialize system
    Plugins->>Loader: Discover available plugins
    loop each plugin
        Loader->>Plugin: Load metadata
        Plugin-->>Loader: Manifest
        Loader->>Plugin: Validate interface compliance
        Plugin-->>Loader: Signature match
    end
    Loader-->>Plugins: Plugin registry
    Plugins-->>Compiler: Ready
```

---

These flows describe the complete process from input project to output package using the MarkDocCompiler execution model.
