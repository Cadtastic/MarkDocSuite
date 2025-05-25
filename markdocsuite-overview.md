# MarkDocSuite Overview

MarkDocSuite is a modular documentation platform for authoring, compiling, and viewing structured Markdown-based content. It is composed of three core applications:

* **MarkDocEditor** – a cross-platform IDE for writing and managing Markdown documentation projects.
* **MarkDocCompiler** – a headless build engine for compiling project files into distributable formats.
* **MarkDocViewer** – a desktop viewer with web & shell extensions for consuming compiled documentation.

---

## Use Case Summary

| Application        | Purpose                                     | Input                        | Output           | 
| ------------------ | ------------------------------------------- | ---------------------------- | ---------------- |
| MarkDocEditor      | Create, edit, and manage projects           | `.mdproj`, `.mbkproj`        | Uses Compiler    |  
| MarkDocCompiler    | Compile structured documentation            | `.mdproj`, `.mbkproj`        | `.mdg`, `.mbk`   | 
| MarkDocViewer      | View compiled documentation (Desktop & Web) | `.mdg`, `.mbk`, `.md`        | Uses Viewer      | 

---

## Supported Formats

| Format     | Description                                         | Consumed By      |
| ---------- | --------------------------------------------------- | ---------------- |
| `.md`      | Individual Markdown file                            | Editor, Viewer   |
| `.mdproj`  | Project file for grouped Markdown collections       | Editor, Compiler |
| `.mbkproj` | Project file for structured long-form documentation | Editor, Compiler |
| `.mdg`     | Markdown Group (static site-like bundle)            | Viewer           |
| `.mbk`     | Markdown Book (feature-rich, indexed book format)   | Viewer           |

---

## Architecture Summary

* Authoring is done in **MarkDocEditor** with live preview, validation, and AI assistance.
* Builds are triggered from the editor or CLI using **MarkDocCompiler**.
* Compiled files are viewed via **MarkDocViewer** or system-integrated preview (Shell Extension).
* The shared plugin system ensures extensibility across all components.

---

MarkDocSuite provides a full documentation workflow from authoring to distribution, built natively on .NET and designed for performance, extensibility, and platform consistency.
