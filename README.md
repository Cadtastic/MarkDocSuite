# MarkDocSuite

MarkDocSuite is a modular platform for creating, compiling, and viewing structured Markdown documentation. It is built for cross-platform delivery using .NET 8 and MAUI, and supports extensibility, CI/CD integration, and AI-powered authoring workflows.

---

## 📦 Components

| Component           | Description                                        |
| ------------------- | -------------------------------------------------- |
| **MarkDocEditor**   | IDE for creating `.mdproj` and `.mbkproj` projects |
| **MarkDocCompiler** | Headless compiler for `.mdg` and `.mbk` output     |
| **MarkDocViewer**   | Desktop, Shell, and Web viewer for output formats  |

---

## 🗂️ File Format Flow

* `.mdproj` → **MarkDocCompiler** → `.mdg`
* `.mbkproj` → **MarkDocCompiler** → `.mbk`
* `.mdg` and `.mbk` → **MarkDocViewer**

---

## 📚 Documentation Index

* [MarkDocSuite Overview](markdocsuite-overview.md)
* [System Architecture](markdocsuite-system-architecture.md)
* [Value Proposition](markdocsuite-value-proposition.md)
* [Change Log](markdocsuite-change-log.md)

### Application Modules

* [MarkDocEditor Documentation](markdoceditor-overview.md)
* [MarkDocCompiler Documentation](markdoccompiler-overview.md)
* [MarkDocViewer Documentation](markdocviewer-overview.md)

---

Start with **MarkDocEditor** to create your first project, then compile with **MarkDocCompiler**, and view the result using **MarkDocViewer**.
