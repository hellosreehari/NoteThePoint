# Project Overview

**notethepoint.online** is a lightweight, single-page rich-text note-taking application designed for speed and beautiful typography. It operates entirely within the browser, storing data locally without the need for a backend server or external database.

**Key Features:**
*   **Rich Text Editor:** A robust, headless WYSIWYG editor currently powered by Quill.js in the background. Note content supports standard headers, blockquotes, bold/italic formatting, and unordered/ordered lists.
*   **Minimalist UI:** The interface consists of an expandable left-side navigation panel (for scanning your notes) and a spacious, distraction-free main editing window on the right.
*   **Dark Mode:** A persistent, polished dark/light theme toggle, accessible from the sidebar and saved in user preferences.
*   **Instant Search:** A search bar built into the sidebar instantly filters existing notes based on matches in the note `title` or `content` fields.
*   **Custom Toolbar:** A custom-styled HTML `.rich-toolbar` integrates seamlessly into the app's dark/light modes without introducing visual clutter, natively mapping to editor formatting options.
*   **Quick Utilities:** Native utilities positioned above the editing window to instantly Print the active note or Copy the raw formatted content successfully to the clipboard.
*   **Accessible Design:** Clean underlying semantic HTML management and CSS overrides crafted particularly to optimize focus, spacing, and readability across both `serif` (body) and `sans-serif` (headers) typography.
*   **Robust Persistence:** All data and rich-text HTML content are rigorously saved and loaded asynchronously from the browser's `IndexedDB` (via localForage) to bypass legacy size limits, while theme preferences remain gracefully inside standard `localStorage`.

# Quick Start Guide

1.  **Add a Note:** Click the "New Note" (Plus Icon) button on the sidebar. This auto-focuses the title field for quick entry.
2.  **Format Content:** Use the rich toolbar dropdown to label lines as Heading 1, Heading 2, Paragraph, or use the quick toggles for bolding/listing. Insert specific URL links using the "Insert Link" pop-up modal.
3.  **Search Everything:** Type your search terms in the sidebar's search box to filter instantly across all notes' contents and titles.
4.  **Manage:** Open the "Delete Note" modal via the trash-can icon in the toolbar or inside the sidebar's note header list.

**Tech Stack:**
*   **Core:** HTML5, CSS3 (Variables, Flexbox), Vanilla JavaScript (ES6+).
*   **Rich Text Engine:** Quill.js Editor (imported headlessly via CDN, stripping away Quill's default UI styling).
*   **Fonts:** Custom Stack (e.g. `sohne`, `source-serif-pro`).
*   **Storage:** Browser IndexedDB (via localForage CDN).

# Building and Running

This project is a standalone static HTML file and does not require a build process or package manager.

**To Run:**
1.  Locate the `index.html` file in the project root.
2.  Open the file in any modern web browser.

# Development Conventions

*   **Structure:** All code (HTML, CSS, JS) is contained within a single `index.html` file for ultimate portability.
*   **Layout & Styling:**
    *   Uses **Flexbox** structurally to manage the main sidebar layout vs the active editor canvas workspace.
    *   The note canvas utilizes `max-width: 900px` to naturally frame the beautiful typography while keeping it legible.
    *   Extensive use of CSS variables (e.g. `--bg-main`, `--text-main`, `--accent-hover`) applied strictly to enable the seamless Dark/Light toggle.
*   **JavaScript & Editor Robustness:**
    *   State is managed via a global `notes` array structured as: `[{ id: string, title: string, content: string, lastModified: number }]`.
    *   Quill initialization inside `initQuill()` runs structurally barebones (`module: { toolbar: false }`), serving solely as the backend DOM parser. Buttons in the `.rich-toolbar` container call custom wrapper functions (`window.formatDoc`) to perform `quill.format()` or `quill.insertText()`, guaranteeing exact visual aesthetics map properly to stable backend text behavior.
    *   `renderSidebar()` and `renderEditor()` sync real-time `text-change` behaviors asynchronously to IndexedDB.