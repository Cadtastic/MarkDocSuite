# MarkDocCompiler Design Requirements

This document defines the functional and technical requirements for MarkDocCompiler. As the core build system for the MarkDocSuite platform, it transforms structured project files into distributable formats using a headless, extensible architecture.

---

## 1. Functional Requirements

### 1.1 Project Compilation

* The system shall compile `.mdproj` into `.mdg` (Markdown Group) format.
* The system shall compile `.mbkproj` into `.mbk` (Markdown Book) format.
* All compilation must be deterministic and file-order predictable.

### 1.2 File Processing

* The system shall use Markdig to parse Markdown content into AST form.
* The AST must support injection and transformation by plugins.
* HTML output shall be constructed from the final AST tree.

### 1.3 Asset Management

* The system shall collect and optimize external files (images, fonts, media).
* Asset references must be updated to reflect packaged paths.

### 1.4 Validation

* All content shall be validated against schema, structural, and formatting rules.
* The system shall reject builds on validation failure unless override is enabled.

### 1.5 Plugin Execution

* C#-based plugins shall be discoverable at runtime.
* Plugins must declare their operation types (e.g., transform, validate).
* Unsafe or unverified plugins shall be blocked unless trusted.

---

## 2. Non-Functional Requirements

### 2.1 Performance

* Compilation of small projects shall complete in <500ms.
* Larger books should complete in <3s with parallelizable phases.

### 2.2 Isolation

* The compiler shall not perform any rendering or UI operations.
* It shall execute in CLI, CI, or programmatic contexts only.

### 2.3 Extensibility

* Plugin APIs shall be exposed via shared interfaces.
* The system shall allow versioned compatibility between compiler and plugins.

---

## 3. Technical Constraints

### 3.1 Runtime Environment

* **.NET 8**, using SDK-style project and MSBuild integration.
* Fully compatible with Windows/macOS build agents.

### 3.2 Output Format Requirements

* `.mdg` shall include a manifest, metadata, documents, and assets.
* `.mbk` shall include navigational index, metadata, structured document sections.

---

## 4. Integration

* The compiler shall be callable from MarkDocEditor.
* It shall support standalone CLI invocation.
* Future versions shall support an API-first invocation path for dynamic systems.

---

These requirements define the boundary between the MarkDocEditor (authoring tool) and the MarkDocCompiler (build engine), allowing them to evolve independently while maintaining a stable contract.
