## Quick orientation

This is a very small, static single-page website. There is no build system, package manager, or server-side code in this workspace. An AI editing agent should treat `html.html` as the single entry point and `style.css` as the primary styling sheet. The image asset `download.jfif` is used as the logo.

Key files
- `html.html` — single-page HTML. Entry point; contains in-page anchor navigation (ids: `about`, `servizi`, `contatti`, `book-a-call`).
- `style.css` — site stylesheet referenced via a relative link in the head.
- `download.jfif` — static asset used for the header logo.

Big-picture architecture (what to know)
- Single static HTML document (no JS). Changes are visible by opening `html.html` in a browser.
- Navigation uses same-page anchors (e.g. `<a href="#about">`), and many headings are wrapped inside anchor tags (example below). Preserve these anchors/ids when editing content or splitting sections.

Concrete examples from the repo
- Headings wrapped in anchors (note: heading inside anchor):

  <a href="#about"><h1 class="header-title">About</h1></a>

- Stylesheet link in the head:

  <link rel="stylesheet" href="style.css">

Project-specific conventions and gotchas
- The repository folder name contains a space (`html css`). When creating paths or shell commands, quote full paths to avoid PowerShell parsing issues.
- Many elements share the class `header-title`; preserve class names when altering header visuals to avoid unexpected styling changes.
- Section navigation relies on element `id` values (`about`, `servizi`, `contatti`, `book-a-call`). If you add or rename a section, update the corresponding anchor(s) in the header area.
- There is no JS behavior to update — any interactive feature you add must include the script file and a careful update to the HTML head.

Developer workflows (quick commands)
- Preview the page by opening the HTML file in the default browser from PowerShell:

```powershell
Start-Process "c:\Users\ACCOUNT SENZA PASS\Desktop\html css\html.html"
```

- Alternatively, use VS Code Live Server extension to get autoreload while editing (recommended for faster feedback). Paths with spaces require quoting.

Editing guidance for an AI agent
- Preserve existing IDs and anchor links unless explicitly refactoring navigation. Example IDs to preserve: `about`, `servizi`, `contatti`, `book-a-call`.
- Keep changes minimal and semantic: prefer editing text nodes and classes in `style.css` for visual changes rather than adding inline styles.
- When adding new sections, add an anchor link in the header block (`.immagineheader`) and a corresponding `id` on the section container so navigation remains consistent.
- Avoid changing the top-level document language (`<html lang="it">`) without confirmation — it influences screen readers and spell check.

PR / commit notes
- This project has no CI; small commits and descriptive messages are preferred. Example: `fix(header): correct anchor id for services`.

When uncertain
- If a requested change touches multiple areas (HTML + CSS + assets), provide a short summary of the edits in the PR body so a human reviewer can verify visual impact.

Questions for the maintainer
- Do you prefer headings wrapped in anchors (current pattern) or anchor-wrapped labels (e.g., `<a><span></span></a>`) for accessibility? If unsure, keep the existing pattern and avoid wide refactors.

If something here is unclear or you want me to include additional patterns (for example, an explicit CSS naming convention or tooling), tell me what to add and I'll update this file.
