# Project Overview

**notethepoint.online** is a lightweight, single-page note-taking application designed for speed and simplicity. It operates entirely within the browser, storing data locally without the need for a backend server or external database.

**Key Features:**
*   **Quick Entry:** Add notes rapidly using a command-line-style interface.
*   **Quick Focus:** Press `/` anywhere to instantly focus the input box and start typing a command.
*   **Interactive Guidance:** Dynamic placeholders and empty states guide new users on using slash commands (e.g., `/work`) to organize notes instantly.
*   **Onboarding:** First-time users are greeted with helpful pinned notes in `#welcome` and `#tips` categories, explaining core features like slash commands and shortcuts.
*   **Categorization:** Organize notes into categories using slash commands (e.g., `/work Project details`). Notes without a command default to the `/general` category.
*   **Mouse Selection:** Users can select categories from the dropdown using the mouse in addition to keyboard navigation.
*   **Symmetric UI:** A centered, fixed-width layout (450px) designed for perfect visual consistency and order, especially for users who value symmetry.
*   **Color Coding:** Consistent, unique colors are generated for each category using a robust hashing algorithm (FNV-1a), appearing in both the search dropdown and the note cards for instant visual recognition.
*   **Dark Mode:** A persistent, polished dark theme (default) for comfortable low-light usage, toggled via a button and saved in user preferences.
*   **Card Pinning:** Pin important categories to the top of the dashboard.
*   **Global Search:** Type `?query` in the input box to instantly filter notes across all categories. The search intelligently matches both note text and category titles.
*   **Polished Animations:** Subtle, non-intrusive animations enhance the UX, including a staggered "waterfall" entry for cards on load, sliding action buttons on hover, and spring-based interactions for theme toggling.
*   **Smart Undo:** Deleting notes or categories shows a non-intrusive "Toast" notification with an instant Undo button, replacing disruptive confirmation dialogs.
*   **Accessible Design:** Semantic HTML (`<h1>`, `<ul>`, `<li>`, `<button>`), ARIA labels, and visible focus states ensure compatibility with screen readers and keyboard navigation.
*   **Robust Persistence:** All data, theme preferences, and layout states are saved to the browser's `localStorage`.

# Quick Start Guide

1.  **Add a Note:** Simply type your note in the input box and press **Enter**. By default, it will be added to the `/general` category.
2.  **Organize with Categories:** To file a note under a specific category, start your input with a slash followed by the category name, then your note: `/work Finish project report`. 
3.  **Quick Focus:** Press the `/` key at any time to instantly jump focus back to the input box.
4.  **Search Everything:** Type `?` followed by your search term to filter notes and category titles instantly: `?report`.
5.  **Pin for Priority:** Use the pin icon on any category card to keep it at the top of your dashboard.

**Tech Stack:**
*   **Core:** HTML5 (Semantic), CSS3 (Variables, Flexbox), Vanilla JavaScript (ES6+).
*   **Fonts:** Google Fonts (Inter).
*   **Storage:** Browser LocalStorage.

# Building and Running

This project is a standalone static HTML file and does not require a build process or package manager.

**To Run:**
1.  Locate the `index.html` file in the project root.
2.  Open the file in any modern web browser.

# Development Conventions

*   **Structure:** All code (HTML, CSS, JS) is contained within a single `index.html` file for portability.
*   **Layout & Symmetry:**
    *   Uses a **Flexbox** layout (`justify-content: center`) to ensure notes grow from the center in a balanced, symmetric fashion.
    *   Cards have a **strictly fixed width (450px)** and stretch vertically within rows to maintain alignment.
    *   Notes feature custom bullet points and subtle separation lines optimized for both light and dark themes.
*   **Styling & Themes:**
    *   Extensive use of CSS variables for theming and consistency.
    *   `getCategoryColor(category)`: Employs an FNV-1a hash to ensure category colors are distinct and deterministic.
*   **JavaScript:**
    *   State is managed in a global `notes` array and a `categoryMeta` object, synced to `localStorage`.
    *   `renderNotes()`: Dynamically generates the symmetric grid, handles sorting (pinned first), and user interactions.
    *   `updateDropdown()`: Provides real-time category suggestions with color-coded previews.
*   **Data Format:**
    *   Notes are stored as objects: `{ id: number, category: string, text: string }`.
    *   Category metadata: `{ [categoryName]: { pinned: boolean, pinnedAt: number } }`.