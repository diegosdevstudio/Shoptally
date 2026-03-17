# Contributing to ShopTally

> **A Smart Shopping List Manager — built by DiegosDevStudio**

Thank you for your interest in contributing! ShopTally is a single-file, open web application with zero dependencies. Every contribution — bug fix, feature idea, or design improvement — is genuinely appreciated.

-----

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [How to Contribute](#how-to-contribute)
- [Development Guidelines](#development-guidelines)
- [Submitting a Pull Request](#submitting-a-pull-request)
- [Reporting Bugs](#reporting-bugs)
- [Feature Requests](#feature-requests)
- [Style Guide](#style-guide)

-----

## Code of Conduct

This project follows a simple rule: **be respectful**. Constructive feedback is welcome; personal attacks are not. Contributors who violate this principle may be removed from the project.

-----

## Getting Started

ShopTally is intentionally dependency-free — there is no build step, no package manager, and no local server required.

### Prerequisites

- A modern browser (Chrome, Firefox, or Edge recommended)
- A code editor (VS Code recommended)
- Git

### Setup

```bash
# 1. Fork the repository on GitHub, then clone your fork
git clone https://github.com/YOUR_USERNAME/shoptally.git

# 2. Navigate into the project
cd shoptally

# 3. Open the app directly in your browser
open ShopTally.html        # macOS
start ShopTally.html       # Windows
xdg-open ShopTally.html    # Linux
```

No `npm install`. No `build`. Just open and code.

-----

## Project Structure

```
shoptally/
├── ShopTally.html      # The entire application (HTML + CSS + JS, single file)
├── README.md           # Project overview and usage guide
├── CONTRIBUTING.md     # This file
└── LICENSE.txt         # License information
```

Everything lives in `ShopTally.html`. The three main sections are clearly commented inside the file:

|Section   |Description                                                    |
|----------|---------------------------------------------------------------|
|`<style>` |All CSS — design tokens, layout, animations, glassmorphism     |
|`<body>`  |HTML structure — nav, list tiles, detail view, modals          |
|`<script>`|All JavaScript — localStorage logic, rendering, receipt builder|

-----

## How to Contribute

### 1. Find something to work on

- Browse [open issues](../../issues) and look for ones labeled `good first issue` or `help wanted`
- Check the [feature requests](#feature-requests) section below
- Spotted a bug? [Report it](#reporting-bugs) first, then fix it

### 2. Create a branch

```bash
# Always branch off main
git checkout main
git pull origin main
git checkout -b feat/your-feature-name
# or
git checkout -b fix/bug-description
```

**Branch naming conventions:**

|Prefix     |Use for                             |
|-----------|------------------------------------|
|`feat/`    |New features                        |
|`fix/`     |Bug fixes                           |
|`style/`   |CSS / visual changes only           |
|`refactor/`|Code cleanup with no behavior change|
|`docs/`    |Documentation updates               |

### 3. Make your changes

- Keep changes focused — one feature or fix per pull request
- Test your changes locally in at least two browsers
- Verify `localStorage` read/write behavior works correctly after your change

### 4. Commit your changes

```bash
git add .
git commit -m "feat: add swipe-to-delete on list tiles"
```

Follow [Conventional Commits](https://www.conventionalcommits.org/) format:

```
type(optional scope): short description

Longer explanation if needed. Wrap at 72 characters.
Explain WHY, not just WHAT.
```

-----

## Development Guidelines

### The Single-File Rule

ShopTally is proudly a single `ShopTally.html` file. **Please do not introduce a build system, external JS files, or npm dependencies** without opening a discussion issue first. External fonts (Google Fonts) and CDN scripts are acceptable.

### AI / API Logic

ShopTally does not currently use an AI API. If a future contribution introduces AI features:

- **Model**: Use `gemini-2.0-flash` for any Gemini integration — do not change without discussion
- **Retry Loop**: Any API call must include a retry loop (3 attempts, 6s delay on 429)
- **JSON Safety**: Strip markdown fences before any `JSON.parse` call
- **API Key**: Must stay in `localStorage` only — never log, transmit, or hardcode it

### CSS / Design System

ShopTally uses a strict design token system via CSS custom properties:

```css
--bg: #121826          /* Page background */
--cyan: #22D3EE        /* Primary accent */
--blue: #2563EB        /* Secondary accent */
--text: #F8FAFC        /* Body text */
--text-muted: #8896AA  /* Secondary / muted text */
```

- **Do not introduce white or light backgrounds** — the dark luxury aesthetic is intentional
- Glassmorphism cards use `backdrop-filter: blur()` — preserve this on all new card elements
- Buttons must use the cyan → blue gradient; solid-color buttons are not permitted

### JavaScript

- Vanilla JS only — no frameworks or libraries
- Use `async/await` for all async operations
- Always wrap async or error-prone operations in `try/catch`
- Keep the `safeParseJSON()` pattern as the single point of JSON parsing if JSON responses are introduced
- Use `localStorage` exclusively for persistence — no IndexedDB, cookies, or external storage

-----

## Submitting a Pull Request

1. Push your branch to your fork:
   
   ```bash
   git push origin feat/your-feature-name
   ```
1. Open a Pull Request against the `main` branch of the upstream repository
1. Fill in the PR template:
- **What does this PR do?**
- **How was it tested?**
- **Screenshots** (if visual changes)
- **Related issue** (e.g. `Closes #12`)
1. A maintainer will review your PR within a few days. Be prepared for feedback and revision requests — this is normal and healthy.

-----

## Reporting Bugs

Before opening a bug report, please:

- Check that you’re using a supported browser
- Confirm `localStorage` is enabled and not blocked by a browser extension
- Search [existing issues](../../issues) to avoid duplicates

When filing a bug, include:

```
**Browser & version:**
**Operating system:**
**Steps to reproduce:**
**Expected behavior:**
**Actual behavior:**
**Console errors (if any):**
```

-----

## Feature Requests

Feature ideas are welcome! Open an issue with the `enhancement` label and describe:

- **The problem** you’re trying to solve
- **Your proposed solution**
- **Alternatives you considered**

Current ideas on the roadmap (up for grabs):

- Export list as PDF or image
- Share a list via URL (state encoded in hash)
- Reorder items via drag-and-drop
- Budget cap per list with over-budget warnings
- AI-powered item suggestions via Gemini

-----

## Style Guide

### HTML

- Use semantic elements (`<section>`, `<nav>`, `<main>`, `<footer>`)
- Keep IDs kebab-case: `id="items-list"`
- Keep classes kebab-case: `class="list-tile"`

### CSS

- Add new design tokens to `:root` — don’t hardcode colors inline
- Group properties: positioning → box model → typography → visual → animation
- Comment non-obvious selectors

### JavaScript

- Use `const` by default, `let` only when reassignment is needed
- Name functions with verbs: `renderDetail()`, `addItem()`, `openReceipt()`
- Keep functions small and single-purpose

-----

## Questions?

Open a [Discussion](../../discussions) or reach out via the issues tab. We’re happy to help you get oriented.

**Built with obsession by [DiegosDevStudio](https://github.com/diegosdevstudio)** ⚡
