# Agent Guide

## Project Overview

Elegant Clock is a zero-dependency static web clock. The whole application lives in `index.html`, with inline HTML, CSS, and JavaScript.

Core behavior:
- Analog clock face with generated hour numbers and rotating hands.
- Digital clock mode with `HH:MM:SS` display.
- Light and dark theme toggle.
- Fullscreen toggle that hides the controls while fullscreen is active.
- About modal with AGPLv3 license information.

## Repository Structure

- `index.html` - Main and only application file. Contains styles, markup, SVG icon strings, and runtime logic.
- `README.md` - Project description, feature list, screenshot, and live demo link.
- `.gitignore` - Currently ignores macOS `.DS_Store` files.

## Development Setup

No install step is required. There is no package manager, bundler, test runner, or framework in this repo.

Recommended local preview options:
- Open `index.html` directly in a browser for quick visual checks.
- Or serve the folder with a tiny local static server, for example `python3 -m http.server 8000`, then open `http://localhost:8000`.

## Coding Conventions

- Keep the project dependency-free unless the user explicitly asks for a larger refactor.
- Prefer small, focused edits inside `index.html`.
- Preserve the existing single-file architecture for simple feature changes.
- Use plain HTML, CSS, and vanilla JavaScript.
- Keep CSS custom properties in `:root` as the source of theme colors.
- Preserve the existing license header comments when editing the CSS or JavaScript sections.
- Use accessible button labels/titles when adding controls.
- Avoid introducing build-only syntax, imports, TypeScript, JSX, or framework-specific code.

## Behavior Notes

- `init()` builds the clock face, starts the one-second update loop, initializes button icons, and registers event listeners.
- `setDate()` drives both analog hand rotation and digital time text.
- `toggleClocks()` switches between analog and digital display states.
- `toggleMode()` changes theme by toggling `body.light-mode`.
- `handleFullscreenChange()` hides controls while fullscreen is active and updates the fullscreen icon.
- The about modal closes only when clicking the overlay background.

## Testing And Verification

There are no automated tests yet. For changes, manually verify:
- Analog hands move and reflect the current time.
- Digital mode updates every second and uses two-digit time parts.
- Analog/digital toggle works repeatedly.
- Light/dark theme toggle updates clock, text, controls, and modal colors.
- Fullscreen enter/exit works and controls hide/show as intended.
- About modal opens and closes by clicking outside the modal content.
- Layout remains usable on desktop and narrow mobile widths.

## Common Change Guidance

- For visual tweaks, update the CSS variables first when possible.
- For new controls, add the button markup, add an icon entry in `icons`, initialize it in `init()`, and register the event listener there.
- For clock behavior changes, start with `setDate()` and keep rendering logic deterministic from a single `Date` instance.
- If a change grows beyond a small enhancement, pause and consider whether the user wants to keep the single-file design or introduce separate CSS/JS files.

## Deployment Notes

The README points to GitHub Pages at `https://frenselw.github.io/elegant-clock/`. Because this is a static site, deployment is likely just the repository contents served by GitHub Pages.
