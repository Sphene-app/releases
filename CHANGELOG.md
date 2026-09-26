# Sphene Kernel v2.1.0 — Verified Plugin Catalog & Enhanced Diff Engine (2026-09-23)

### Verified Plugin Catalog & Enhanced Diff Engine
* **Verified Plugin Catalog**: 1-click installation, verification badges, and dynamic capability registration.
* **PR-Style Inline Diff**: Visual inline diff viewer for file revisions with explicit line-level accept/veto actions.
* **Dynamic Partition Scoping**: Dynamic boundary previews in the editor ensuring strict workspace isolation.
* **Smart Update Installer**: Auto-detects running daemon instances and seamlessly updates binaries without downtime.

---

# Sphene Kernel v2.0.0 — Hardened Go Engine & Autonomous PWA Shell (2026-09-22)

### Sphene Hardened Knowledge Kernel v2.0
* **Go Kernel Core Architecture**: Complete engine rewrite in high-performance Go with zero runtime dependencies.
* **Autonomous PWA Shell**: Fully autonomous local Progressive Web App running entirely offline from client storage.
* **Embedded SQLite FTS5 Index**: Sub-millisecond full-text vault search and metadata indexing.
* **Differential Timeline V2**: Native PR-style diff engine with accept/veto controls for agent proposed modifications.
* **Zero-Trust Plugin Sandbox**: Isolated WebAssembly/WASI plugin runtime preventing unauthorized network access.

---

# Sphene v1.4.0 — Distraction-Free Read Mode & Sovereign PDF Export (2026-09-20)

### Read Mode & Sovereign PDF Export
* **True Distraction-Free Read Mode**: Collapsible chrome and navigation maximizing typographic focus.
* **Sovereign PDF Engine**: Print and export documents to clean, publication-ready PDF preserving custom themes and math formulas.
* **Document Outline HUD**: Interactive floating table-of-contents drawer for effortless navigation through lengthy notes.
* **Reading Progress Bar**: Subtle visual reading indicator tracking document scroll position.

---

# Sphene v1.3.0 — Semantic Link Inference & Real-Time Vault Linter (2026-09-19)

### Semantic Link Inference & Linting
* **Semantic Link Inference**: Intelligent recommendations for related notes based on content analysis and shared concept vectors.
* **Vault Integrity Linter**: Continuous background checking for broken internal links, orphaned media, and empty headings.
* **Dead Link Resolver**: 1-click automated refactoring to repair renamed document references across the entire vault.
* **Heading Structure Validator**: Warnings for skipped heading levels to ensure accessible, clean document outlines.

---

# Sphene v1.2.0 — Sovereign Vector Canvas & Freehand Drawing Notes (2026-09-18)

### Sovereign Vector Canvas & Drawing
* **Dedicated Drawing Notes**: Native `.drawing` note type with instant vector freehand sketching.
* **Multi-Touch & Stylus Support**: Pressure-sensitive stroke rendering, color palettes, stroke width selector, and vector eraser.
* **Pinch-to-Zoom & Pan HUD**: Smooth 60fps pan and zoom navigation across infinite canvas space.
* **Vector SVG/PNG Export**: 1-click export and seamless embedding into standard Markdown documents.

---

# Sphene v1.1.0 — Native Mermaid Diagrams & KaTeX Math Typesetting (2026-09-17)

### Rich Technical Diagrams & Mathematics
* **Native Mermaid Rendering**: Flowcharts, sequence diagrams, state diagrams, and entity-relationship diagrams rendered directly in preview.
* **KaTeX Mathematics**: Full LaTeX math formula typesetting for inline `$formula$` and block `$$formula$$` equations.
* **Interactive Markdown Tables**: Column alignment, visual sorting, and automated cell formatting.
* **HTML Sanitization Pipeline**: Strict DOMPurify sanitization preventing script injection in rendered output.

---

# Sphene v1.0.0 — Native Model Context Protocol (MCP) Architecture (2026-09-15)

### Model Context Protocol (MCP) Server Architecture
* **Native MCP Server**: Replaced ad-hoc scripts with standardized JSON-RPC 2.0 Model Context Protocol interface.
* **Comprehensive Tool Surface**: Vault search, note read/write, differential timeline, and knowledge graph tools for AI agents.
* **Zero-Source-Leakage Security Boundary**: Full read-only guardrails and staged proposal workflows protecting human vaults from unprompted overwrite.
* **Universal Client Compatibility**: Plug-and-play interoperability with Claude Code, Cursor, Hermes Agent, OpenClaw, and Gemini CLI.

---

# Sphene v0.9.0 — Vault Migration Toolkit & Media Transclusion (2026-09-12)

### Migration & Media Engine
* **1-Click Vault Migration**: Zero-data-loss importer for standard desktop Markdown vaults (.zip archives or local directories).
* **Media Transclusion Engine**: Seamless inline rendering of `![[image.png]]`, audio clips, and embedded PDF pages.
* **Visual Canvas Importer**: Automatic conversion of visual `.canvas` whiteboard files into connected Markdown index maps.
* **Standalone Migration CLI**: Independent `migrate_vault.py` and `migrate_vault.sh` scripts for batch headless migrations.

---

# Sphene v0.8.0 — Interactive Checklists & Frontmatter Metadata (2026-09-05)

### Interactive Checklists & Frontmatter
* **Interactive Task Checklists**: Clickable `- [ ]` and `- [x]` checkboxes that update markdown files atomically in-place without opening the editor.
* **YAML Frontmatter Parser**: Visual property chips for tags, dates, author, and status defined in document YAML headers.
* **Template Generator**: Configurable boilerplate templates for meeting notes, research papers, and project plans.
* **Smart Daily Notes**: Instant shortcut to today's daily log with automatic backlink injection.

---

# Sphene v0.7.0 — Dynamic Crystals Theme Engine & Command Palette (2026-08-28)

### Dynamic Crystals Theming
* **Dynamic Crystals Theme Engine**: Instant zero-reload switching between curated color palettes (Obsidian Dark, Emerald Crystal, Nord, Amber, Pure White).
* **CSS Custom Properties Tokens**: Full semantic theming architecture adhering strictly to high-contrast WCAG guidelines.
* **Global Command Palette**: Instant keyboard navigation (`Ctrl+P` / `Cmd+P`) for accessing all commands, notes, and settings.
* **Custom CSS Snippets**: Support for user-defined CSS overrides stored directly in the vault.

---

# Sphene v0.6.0 — Word Counter, Typewriter Scrolling & Typography Polish (2026-08-18)

### Core Utilities & Editor Ergonomics
* **Live Metrics HUD**: Real-time word count, character count, and estimated reading time meters in the editor footer.
* **Typewriter Scrolling**: Keeps the active cursor line vertically centered for ergonomic long-form writing.
* **Typography Engine**: Native Google Fonts loading (Inter, JetBrains Mono, Outfit) with custom line-height and letter-spacing options.
* **Focus Mode**: Dimming of inactive paragraphs to highlight the active sentence.

---

# Sphene v0.5.0 — Sovereign Knowledge Graph & Tag Taxonomy (2026-08-05)

### Sovereign Knowledge Graph
* **Force-Directed Knowledge Graph**: Interactive visual canvas representing vault document nodes and relationship vectors.
* **Hierarchical Tag Taxonomy**: Deep nested tag indexing (`#research/systems/crypto`) with visual graph clustering.
* **Orphan & Dangling Link Discovery**: Automated detection of dead references and unlinked notes across the entire vault.
* **Neighborhood Filtering**: Dynamic graph depth filtering centered on the currently active note.

---

# Sphene v0.4.0 — Differential Timeline Engine & Micro-Snapshots (2026-07-22)

### Differential Timeline & Change Tracking
* **Micro-Snapshotting**: Automatic fine-grained change tracking on every note edit without git repository overhead.
* **Visual Diff Inspector**: Unified split-view visual difference viewer showing added and removed lines.
* **1-Click Rollback**: Instant restoration of previous document states from the local historical timeline.
* **Tamper-Evident History**: Cryptographic change logs recording both human and agent edits.

---

# Sphene v0.3.0 — Dynamic Plugin Architecture & Extension Slots (2026-07-08)

### Dynamic Extensibility Engine
* **Inversion-of-Control Plugin Architecture**: Modular extension points for custom renderers, sidebars, and commands.
* **Safe Runtime Sandbox**: Zero-eval plugin execution context preventing script injection and vault corruption.
* **Hot-Reload Capabilities**: Instant dynamic activation and deactivation of plugins without restarting the host.
* **Lifecycle Hooks**: Complete hook events for note loading, saving, rendering, and indexing.

---

# Sphene v0.2.0 — Agent Integration & Sandboxed Scratchpads (2026-06-25)

### Agent Integration Foundation
* **Hermes Agent Integration**: Automated background note organization and smart categorization via CLI skill triggers.
* **Sandboxed Agent Scratchpads**: Dedicated system directories (`00_System/`, `10_SecondBrain/`) strictly separating agent working memory from human writing spaces.
* **Permission Boundaries**: Read-only human partition guarantees to prevent unprompted agent modifications.
* **Daily Brief Engine**: Automated daily summary synthesis from active vault tasks and recent notes.

---

# Sphene v0.1.0 — Genesis: Local Markdown Core & Bi-Directional Links (2026-06-10)

### Genesis of Sovereign Knowledge Workspace
* **Local-First Markdown Core**: Complete raw file backing; notes stored as plain `.md` files without proprietary lock-in.
* **Bi-Directional Wikilinks**: Native `[[document]]` link resolution and forward-link indexing.
* **Real-Time Split Preview**: Instant Markdown rendering with syntax highlighting for code blocks.
* **Vault Explorer**: Clean hierarchical file navigation with instant folder tree synchronization.

---

