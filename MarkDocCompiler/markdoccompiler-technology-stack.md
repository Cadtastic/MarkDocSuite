# MarkDocCompiler Technology Stack

This document defines the technologies and frameworks used to implement MarkDocCompiler. The system is designed as a headless, high-performance compilation engine integrated with MarkDocEditor or external build systems.

---

## Platform

* **.NET 8**
  Core runtime environment for executing the compiler as a native console or service process.

---

## Languages

* **C#**
  Used for all compiler logic, validation, transformation, and packaging routines.

---

## Markdown Engine

* **Markdig**
  High-performance .NET Markdown processor that converts Markdown to AST and then to HTML.

  * Supports GitHub Flavored Markdown
  * Enables AST inspection and transformation

---

## Packaging Targets

* **.mdg** (Markdown Group)

  * Output format compiled from `.mdproj`
  * Contains bundled Markdown documents and referenced static assets
  * Layout and structure suitable for static viewing environments

* **.mbk** (Markdown Book)

  * Output format compiled from `.mbkproj`
  * Structured, searchable document with navigation metadata and internal linking
  * Suitable for long-form, book-style help and software or product documentation delivery

---

## Build and Execution

* **MSBuild + .NET SDK**
  Used to compile and package the MarkDocCompiler application.

* **Command Line Interface (CLI)**
  Headless execution for integration with CI pipelines and automation scripts.

* **API-Ready Architecture**
  Internals are structured for future exposure via programmatic interfaces or web APIs.

---

## File Format Support

* **Inputs**:

  * `.mdproj`, `.mbkproj`
  * Markdown `.md`, asset files, metadata files

* **Outputs**:

  * `.mdg` (Markdown Group)
  * `.mbk` (Markdown Book)

---

## Dependencies and Integration

* **Shared Plugin System**
  Supports C# plugins that operate on Markdown AST or affect package output.

* **Compatible with MarkDocEditor**
  Designed to be invoked by MarkDocEditor as the backend compiler.

---

This technology stack ensures that MarkDocCompiler is lightweight, extensible, and automation-ready for both desktop and headless build environments.
