# Contributing to NoteThePoint

Thank you for your interest in contributing to **NoteThePoint**! We welcome community contributions that help make this notepad faster, more accessible, and more useful while adhering strictly to our local-first, zero-knowledge privacy philosophy.

---

## 🧭 Code of Conduct & Guiding Philosophy

When contributing to NoteThePoint, please keep our core tenets in mind:
1. **Zero Tracking / Zero Backend:** We do not accept features that transmit user keystrokes, personal notes, or identifiable metadata to third-party endpoints.
2. **Performance First:** Everything must run instantaneously without bloat. Avoid adding heavy client-side frameworks or large external dependencies.
3. **Accessibility & Clean Semantics:** All interactive elements must support keyboard navigation, standard ARIA labels, and readable contrast across dark and light themes.

---

## 🛠️ How to Contribute

### 1. Reporting Bugs
- Search existing [GitHub Issues](https://github.com/hellosreehari/NoteThePoint/issues) to verify the bug hasn't already been reported.
- If it hasn't, open a new issue detailing:
  - Your browser and operating system version.
  - Clear steps to reproduce the issue.
  - Expected vs. actual behavior.

### 2. Suggesting Enhancements
- Open a feature request issue describing the use case and why it benefits privacy-conscious note-takers.
- Please discuss significant changes before submitting large pull requests.

### 3. Submitting Pull Requests
1. **Fork** the repository and clone your fork locally.
2. Create a clean feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Make your changes adhering to existing coding conventions (semantic HTML5, vanilla JavaScript, CSS variables).
4. Test thoroughly across Chrome, Safari, and Firefox. Ensure Dark Mode toggle and mobile responsiveness function properly.
5. Verify JSON-LD schemas and internal relative links:
   ```bash
   node -e '
   const fs = require("fs");
   const path = require("path");
   // Validate HTML and JSON-LD
   '
   ```
6. Commit with a clear, descriptive message:
   ```bash
   git commit -m "Add keyboard shortcut for strike-through formatting"
   ```
7. Push to your fork and submit a **Pull Request** to `main`.

---

## 🎨 Coding Conventions

- **HTML/CSS/JS:** Pure standards-based code. No build steps (Webpack/Vite) or runtime dependencies beyond lightweight CDNs (Quill.js, localForage).
- **CSS Variables:** All colors must reference CSS variables defined in `:root` and `body.dark-theme` so dark mode functions without visual regressions.
- **State Management:** Note state is persisted via `localForage` (IndexedDB). Never store sensitive note contents in unencrypted remote storage.

Thank you for helping keep NoteThePoint fast, open, and private!
