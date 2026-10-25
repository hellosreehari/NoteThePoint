<div align="center">

# NoteThePoint ✍️

**A fast, private, distraction-free online notepad and rich-text writing workspace.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Zero Backend](https://img.shields.io/badge/Backend-Zero%20(Client--Side)-success.svg)](https://notethepoint.online)
[![Storage](https://img.shields.io/badge/Storage-Browser%20IndexedDB-orange.svg)](https://notethepoint.online)
[![Live Site](https://img.shields.io/badge/Live-notethepoint.online-emerald.svg)](https://notethepoint.online)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

[**Launch Notepad**](https://notethepoint.online) • [**Read the Blog**](https://notethepoint.online/blog/) • [**About & Architecture**](https://notethepoint.online/about.html) • [**Report an Issue**](https://github.com/hellosreehari/NoteThePoint/issues)

</div>

---

## 📖 Overview

**NoteThePoint** is an open-source, local-first web notepad engineered to eliminate digital friction. What should be the simplest human computing interaction—jotting down a phone number, organizing meeting thoughts, drafting a technical essay, or formatting code snippets—often requires multi-gigabyte software, mandatory cloud logins, password fatigue, and data tracking.

NoteThePoint runs **100% in your browser**. It requires **zero sign-up**, possesses **zero backend databases**, and commits all your writing directly to your browser's sandboxed **IndexedDB** storage.

---

## ✨ Key Features

- **🚀 Instant Speed (< 50ms):** Open the tab and start typing immediately. No login modals, onboarding checklists, or account paywalls.
- **🔒 Zero-Knowledge Privacy:** Keystrokes and notes never cross a network interface. Data lives exclusively on your local disk.
- **💾 Offline-First Fidelity:** Runs seamlessly in airplane mode or during network outages. Powered by local IndexedDB transactional storage.
- **🎨 Distraction-Free Typography:** Carefully curated editorial font stacks, proportional line heights, and an instant **Dark / Light theme** toggle.
- **📝 Headless Rich-Text Engine:** Full support for Headings (H1, H2, H3), blockquotes, bold/italic formatting, bulleted and ordered lists, and hyperlinks.
- **🔍 Sub-Millisecond Search:** Instant debounce-filtered full-text search across titles and body contents.
- **🖨️ Clean Export & Print:** Built-in one-click clipboard copying and `@media print` optimized PDF generation.
- **📚 Integrated Publication:** Accompanied by 13 in-depth engineering guides covering browser storage, privacy laws, and cognitive productivity.

---

## 🏛️ Architecture & Privacy Model

```
+-------------------------------------------------------------+
|                     Client Web Browser                      |
|                                                             |
|   +-------------------+          +----------------------+   |
|   |   Quill.js DOM    | <======> | Custom Rich Toolbar  |   |
|   |  Headless Engine  |          | & Keyboard Shortcuts |   |
|   +-------------------+          +----------------------+   |
|             |                                               |
|             v                                               |
|   +-----------------------------------------------------+   |
|   |   State Manager (Debounced Autosave & Search)       |   |
|   +-----------------------------------------------------+   |
|             |                                               |
|             v                                               |
|   +-----------------------------------------------------+   |
|   |   localForage / Browser IndexedDB (Local Storage)   |   |
|   +-----------------------------------------------------+   |
+-------------------------------------------------------------+
                              ||
                    [ ZERO NETWORK EGRESS ]
                              ||
                              v
                  X  Remote Cloud Databases
                  X  Account Tracking APIs
                  X  Server-Side Keystroke Logging
```

1. **Storage Subsystem:** Instead of fragile 5MB `localStorage`, NoteThePoint employs **IndexedDB** (via localForage). This allows persistent, structured storage with hundreds of megabytes of quota per origin without blocking the main rendering thread.
2. **Ephemeral Incognito Mode:** Opening NoteThePoint in an Incognito/Private window provides a completely sandboxed scratchpad that physically purges its database upon closing the window.

---

## 📁 Repository Structure

```text
NoteThePoint/
├── .github/
│   ├── workflows/          # CI/CD deployment pipelines (Azure Static Web Apps)
│   └── ISSUE_TEMPLATE/     # Standardized GitHub issue templates
├── blog/                   # Technical publication (13 comprehensive guides)
│   ├── index.html          # Blog catalog & category navigation
│   └── *.html              # Standalone deep-dive articles
├── index.html              # Core application & crawlable landing page
├── about.html              # Technical architecture, testing standards & founder bio
├── contact.html            # Community support & GitHub inquiry routing
├── privacy.html            # Privacy policy & AdSense cookie disclosures
├── terms.html              # Terms of service
├── 404.html                # Custom 404 error page
├── sitemap.xml             # XML sitemap with all 18 routes
├── robots.txt              # Crawler rules for Googlebot & Mediapartners
├── og-image.png            # OpenGraph 1200x630 social card
├── favicon.svg             # Vector site icon
├── LICENSE                 # Open source MIT License
├── CONTRIBUTING.md         # Guidelines for open source contributors
├── SECURITY.md             # Vulnerability disclosure policy
└── README.md               # Project documentation
```

---

## 🛠️ Tech Stack

- **Frontend Core:** Semantic HTML5, CSS3 Custom Properties (Variables), Vanilla JavaScript (ES6+).
- **Editor Engine:** [Quill.js](https://quilljs.com/) (Headless integration via CDN with custom formatting handlers).
- **Client Storage:** [localForage](https://localforage.github.io/localForage/) (IndexedDB abstraction).
- **Hosting & CI/CD:** GitHub Actions & Azure Static Web Apps.
- **Zero Build Tools:** Runs natively in any modern browser without Webpack, Vite, or npm compilation steps.

---

## 🚀 Quick Start (Local Development)

Because NoteThePoint is built with vanilla web standards, it requires no package manager or build step.

### Option 1: Python Simple Server
```bash
# Clone the repository
git clone https://github.com/hellosreehari/NoteThePoint.git
cd NoteThePoint

# Start a local static server
python3 -m http.server 8080
```
Open [http://localhost:8080](http://localhost:8080) in your web browser.

### Option 2: Node.js `npx serve`
```bash
npx serve .
```

---

## 🧪 Validation & Integrity Checks

To ensure all JSON-LD microdata, Article schemas, and internal navigation links are valid, run the built-in Node.js verification script:

```bash
node -e '
const fs = require("fs");
const path = require("path");

function getHtmlFiles(dir) {
    let results = [];
    fs.readdirSync(dir).forEach(file => {
        const full = path.join(dir, file);
        if (fs.statSync(full).isDirectory()) results = results.concat(getHtmlFiles(full));
        else if (file.endsWith(".html")) results.push(full);
    });
    return results;
}

getHtmlFiles(".").forEach(f => {
    const content = fs.readFileSync(f, "utf-8");
    const jsonLdRegex = /<script type="application\/ld\+json">([\s\S]*?)<\/script>/gi;
    let match;
    while ((match = jsonLdRegex.exec(content)) !== null) {
        JSON.parse(match[1]);
    }
});
console.log("All HTML files and JSON-LD schemas validated successfully!");
'
```

---

## 🤝 Contributing

Contributions, bug reports, and suggestions are warmly welcomed! Please read our [**Contributing Guide**](CONTRIBUTING.md) to get started.

1. Fork the Project.
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`).
3. Commit your Changes (`git commit -m "Add AmazingFeature"`).
4. Push to the Branch (`git push origin feature/AmazingFeature`).
5. Open a Pull Request.

---

## 📄 License

Distributed under the **MIT License**. See [`LICENSE`](LICENSE) for more information.

---

## 👤 Author & Maintainer

**Sreehari A**
- **GitHub:** [@hellosreehari](https://github.com/hellosreehari)
- **Live Project:** [notethepoint.online](https://notethepoint.online)
