# Security Policy

## Supported Versions

| Version | Supported |
| :--- | :--- |
| Latest (`main` branch) | ✅ Yes |
| Older releases | ❌ No |

---

## 🔒 Architectural Security Model

NoteThePoint operates under a **client-side zero-knowledge architecture**:
- **No Remote Database:** All user writing and documents are stored exclusively in the user's browser via **IndexedDB**.
- **No Keystroke Egress:** Keystrokes, drafts, and notes are never transmitted over the network to any server.
- **Client Sandboxing:** The browser's Same-Origin Policy isolates IndexedDB storage from third-party sites.

---

## 🛡️ Reporting a Vulnerability

If you discover a security vulnerability or potential privacy leak (e.g., unintended network egress, DOM-based Cross-Site Scripting, or storage leakage):

1. **Do not disclose the issue publicly.**
2. Please open a security advisory or report the issue privately via [GitHub Security Advisories](https://github.com/hellosreehari/NoteThePoint/security/advisories) or submit an issue on our [GitHub repository](https://github.com/hellosreehari/NoteThePoint/issues).
3. Include detailed steps to reproduce the vulnerability, including browser version and proof-of-concept payload if applicable.

We take privacy and client security seriously and will investigate and address reported issues promptly.
