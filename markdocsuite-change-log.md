# MarkDocSuite Change Log

## Version 0.0.2

### 🔄 System Architecture Updates

* Finalized `.mdproj → .mdg` and `.mbkproj → .mbk` format transition.
* MarkDocCompiler now handles all compilation from project files to distributable outputs.
* MarkDocEditor introduced as a dedicated IDE for authoring, validating, and invoking builds.
* MarkDocViewer limited to reading `.md`, `.mdg`, and `.mbk` outputs only.
* Shell Extension updated to preview `.md`, `.mdg`, and `.mbk` (no longer `.mdproj`/`.mbkproj`).

### 📦 File Format Changes

* `.mdproj` and `.mbkproj` are no longer previewable formats—they are strictly internal to MarkDocEditor.
* `.mdg` now represents a grouped markdown package for navigation-based viewing.
* `.mbk` now represents a compiled book-format package similar to `.chm`.

### 📁 Component Separation

* MarkDocCompiler converted to a headless CLI/API-first build engine.
* MarkDocEditor added as a standalone, authoring-focused IDE.
* MarkDocViewer simplified to focus on viewing and consuming compiled formats.

### 🧠 Updated Documentation

* All documents across MarkDocCompiler, MarkDocEditor, and MarkDocViewer were rewritten to reflect new format roles and separation of responsibilities.
* Mermaid diagrams, rendering pipelines, and plugin injection flows updated accordingly.

---

Prior version: \[v0.0.1] — Initial documentation draft
