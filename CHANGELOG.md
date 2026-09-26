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

