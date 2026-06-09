# Project Pulse Dashboard Implementation Plan

## Summary

Build Mona's Project Pulse dashboard as a lightweight, static web application with three core deliverables: a polished HTML dashboard page with project cards, semantic CSS styling with visual affordances, and a JSON data structure. The Planner identifies file ownership, parallel work opportunities, and validation checkpoints. The Designer guides UI/UX and visual hierarchy. The Coder implements all application files and the VS Code launch configuration.

## Ordered Implementation Steps

### Phase 1: Data Structure Foundation
**Step 1.1: Create `app/project-data.json`**
- File: `app/project-data.json` (Coder responsibility)
- Define a `projects` array with sample project objects
- Each project includes: `name`, `owner`, `status`, `recentActivity`, `priority`
- Include 3–5 example projects with realistic data
- Validate JSON is parseable and complete

### Phase 2: Design System & Styling (Parallel with Phase 1)
**Step 2.1: Design information hierarchy and visual system**
- File: `app/styles.css` (Designer responsibility)
- Identify key UI components: `.dashboard` container, `.project-card`, status badges, priority indicators
- Define color palette, typography, spacing, and responsive breakpoints
- Design decisions: card-based layout, visible status badges, readable spacing, rounded corners, shadows

**Step 2.2: Implement `app/styles.css`**
- File: `app/styles.css` (Coder responsibility, informed by Designer)
- Create base reset and utility styles
- Style `.dashboard` (grid layout, padding, background)
- Style `.project-card` (padding, border-radius, box-shadow, hover states)
- Style status badges, priority indicators, owner/activity text
- Ensure responsive behavior for smaller viewports
- Include visual affordances: shadows, borders, contrast, typography hierarchy

### Phase 3: HTML Markup & Application Logic (Dependent on Phases 1 & 2)
**Step 3.1: Create `app/index.html`**
- File: `app/index.html` (Designer for layout/hierarchy, Coder for implementation)
- Create semantic HTML structure with `<header>`, `<main>`, and `<footer>`
- Add `<title>Project Pulse</title>` and meta tags
- Link `styles.css` and include inline or external JavaScript to fetch/render data
- Create a `<div class="dashboard">` container for project cards
- Build a template or loop structure to render `.project-card` elements
- For each card: display project name, owner, status badge, recent activity, priority level
- Fetch data from `project-data.json` and render cards dynamically
- Ensure no console errors and page renders without a server (or gracefully loads JSON)

### Phase 4: Tooling & Launch Configuration (Parallel with Phase 3)
**Step 4.1: Create `.vscode/launch.json`**
- File: `.vscode/launch.json` (Coder responsibility)
- Define **Run Project Pulse Dashboard** launch configuration
- Use `python -m http.server` or Node.js `npx http-server` as the server
- Set `cwd` to `${workspaceFolder}/app`
- Configure to serve `index.html` (not a directory listing)
- Open `http://localhost:8000/index.html` (or configured port) automatically
- Include deterministic port assignment (e.g., 8000)

## File Assignments

| File | Responsible Agent | Phase | Dependency |
|------|------------------|-------|-----------|
| `app/project-data.json` | Coder | 1 | None |
| `app/styles.css` | Designer (design), Coder (implementation) | 2 | None (parallel with Phase 1) |
| `app/index.html` | Coder (implementation), Designer (review) | 3 | `app/project-data.json`, `app/styles.css` |
| `.vscode/launch.json` | Coder | 4 | `app/index.html`, `app/styles.css`, `app/project-data.json` |

## Dependencies Between Steps

```
Phase 1 (Data)           Phase 2 (Design/CSS)
   ↓                            ↓
   └────────────┬───────────────┘
                ↓
           Phase 3 (HTML)
                ↓
           Phase 4 (Launch Config)
```

- **Phase 1 → Phase 3**: HTML must reference and fetch `project-data.json`
- **Phase 2 → Phase 3**: HTML must link `styles.css` for styling to apply
- **Phase 3 & 2 → Phase 4**: Launch config depends on final `index.html` and CSS
- **Phase 1 & 2**: Can start in parallel; no direct dependency

## Work That Can Run in Parallel

1. **Designer designs `app/styles.css`** while **Coder builds `app/project-data.json`**
   - Designer creates visual system, component specs, CSS class hooks (`.dashboard`, `.project-card`, etc.)
   - Coder structures JSON data schema and sample projects
   - Handoff: Designer provides CSS specifications; Coder implements and validates both JSON and CSS

2. **Designer reviews HTML layout** while **Coder implements `app/index.html`**
   - Designer ensures information hierarchy, accessibility, responsive behavior
   - Coder writes semantic markup and JavaScript to render cards

## Work That Must Run Sequentially

1. **`app/project-data.json` → `app/index.html`**: HTML must reference the data file and fetch it
2. **`app/styles.css` → `app/index.html`**: HTML must link the CSS file before rendering
3. **All app files → `.vscode/launch.json`**: Launch configuration depends on complete, working `index.html`

## Designer Responsibilities

1. **Information Hierarchy**
   - Identify what project information is most important: name, status, owner, activity, priority
   - Order visual emphasis: status badges most prominent, owner/activity secondary

2. **Visual Design System**
   - Define color palette for status badges (e.g., green=active, yellow=at-risk, red=blocked)
   - Define typography: heading sizes, font family, line-height, contrast
   - Define spacing: card padding, gap between cards, dashboard margins

3. **Component Specification**
   - `.dashboard`: grid layout (e.g., 2–3 columns, responsive to 1 on mobile), centered, readable max-width
   - `.project-card`: card-based design with rounded corners, shadow, hover lift effect
   - Status badge styling: background color + text color for accessibility
   - Priority indicator: text label or icon with clear visual distinction

4. **Accessibility & Usability**
   - Ensure sufficient color contrast for all text
   - Use semantic HTML (headers, sections) for screen readers
   - Provide alt text or ARIA labels for status/priority indicators
   - Test responsive design on common breakpoints (mobile, tablet, desktop)

5. **Design Decisions & Tradeoffs**
   - Choose between icon-based vs. text-based status (text is more universally understood; icons need labels)
   - Choose card layout over table: more mobile-friendly, better visual hierarchy
   - Prioritize readable spacing and breathing room over cramming more data

## Coder Responsibilities

1. **`app/project-data.json` Structure**
   - Create a `projects` array
   - Each object must include: `name`, `owner`, `status`, `recentActivity`, `priority`
   - Ensure valid JSON (no trailing commas, properly quoted strings)
   - Include 3–5 realistic example projects with varied statuses and priorities

2. **`app/styles.css` Implementation**
   - Implement all Designer-specified styles from visual system
   - Create deterministic CSS selectors (`.dashboard`, `.project-card`, `.status-badge`, `.priority-label`)
   - Ensure no browser warnings or deprecated properties
   - Test on at least two browsers (e.g., Chrome, Firefox)
   - Validate CSS syntax

3. **`app/index.html` Implementation**
   - Create semantic HTML5 structure
   - Include `<title>`, meta tags for viewport and character encoding
   - Link `styles.css` with a relative or absolute path that works in the app directory
   - Use JavaScript (vanilla, no external libraries required) to:
     - Fetch `project-data.json` with `fetch()` API
     - Parse and render `.project-card` elements for each project
     - Display `name`, `owner`, `status`, `recentActivity`, `priority` in a readable layout
   - Include error handling for fetch failures (e.g., "Failed to load projects")
   - Ensure no console errors on page load
   - Test opening the file directly (`file:///path/to/app/index.html`) or via HTTP server

4. **`.vscode/launch.json` Configuration**
   - Create the `.vscode` directory if it does not exist
   - Define a launch configuration with:
     - `"name": "Run Project Pulse Dashboard"`
     - `"type": "python"` (if using `python -m http.server`) or `"node"` (if using Node.js server)
     - `"request": "launch"`
     - `"cwd": "${workspaceFolder}/app"`
     - `"command"`: `python -m http.server 8000` or equivalent
     - `"url": "http://localhost:8000/index.html"` (to open the dashboard, not a directory listing)
     - Deterministic port (e.g., 8000)
   - Ensure the configuration is strict JSON (no comments)
   - Test the launch configuration by clicking **Run** in VS Code and verifying the dashboard opens

5. **Validation & Testing**
   - Test that `index.html` renders without JavaScript errors
   - Test that CSS applies (colors, spacing, card layout visible)
   - Test that JSON data loads and cards populate correctly
   - Test launch configuration opens the dashboard (not a directory listing)
   - Verify responsive design works on at least one smaller viewport (e.g., mobile-simulated in DevTools)

## Edge Cases to Handle

1. **Missing or malformed `project-data.json`**
   - Fallback: Display a friendly error message or sample projects
   - Handler: `fetch()` error, try/catch on JSON parse

2. **Empty `projects` array`**
   - Display a message like "No projects found" instead of a blank dashboard

3. **Missing fields in project object** (e.g., owner is null/undefined)
   - Fallback to placeholder text (e.g., "Unassigned", "No activity yet")

4. **Long project names or owner names**
   - Use CSS text truncation (`text-overflow: ellipsis`, `white-space: nowrap`) or word wrapping
   - Test with long strings to ensure cards don't break layout

5. **CSS fails to load**
   - HTML should still be readable (semantic markup provides fallback)
   - Provide a console warning if CSS fetch fails

6. **Browser compatibility**
   - Support modern browsers (Chrome, Firefox, Safari, Edge)
   - Use `fetch()` API (supported in all modern browsers; IE requires polyfill, but IE is out of support)
   - Avoid ES2020+ features; target ES2015 (ES6) for broader compatibility

7. **Different screen sizes and orientations**
   - Mobile (< 480px): Single-column layout
   - Tablet (480px–1024px): Two-column layout
   - Desktop (> 1024px): Two to three-column layout
   - Test with at least one mobile breakpoint

8. **Accessibility failures**
   - Status/priority indicators must have sufficient color contrast
   - Interactive elements (if any, e.g., hover states) must be clear
   - Screen reader users must understand card structure (use semantic HTML, ARIA if needed)

## Validation Expectations

### Data (`app/project-data.json`)
- ✓ File parses as valid JSON (no syntax errors)
- ✓ Contains a `projects` array
- ✓ Each project has `name`, `owner`, `status`, `recentActivity`, `priority` fields
- ✓ At least 3 sample projects with realistic, varied data

### Styling (`app/styles.css`)
- ✓ CSS syntax is valid (no errors in DevTools console)
- ✓ Includes `.dashboard` class with grid layout or similar
- ✓ Includes `.project-card` class with visual affordances (rounded corners, shadow, padding)
- ✓ Includes styling for status badges (background + text colors)
- ✓ Responsive design: cards adapt to smaller screens
- ✓ Typography is readable (font size, contrast, line-height)

### Markup (`app/index.html`)
- ✓ HTML5 semantic structure (`<header>`, `<main>`, `<section>`, etc.)
- ✓ `<title>` is "Project Pulse" or similar
- ✓ Links `styles.css` correctly
- ✓ Includes inline JavaScript or external script to fetch and render `project-data.json`
- ✓ Renders project cards for each project with all required fields visible
- ✓ No console errors when page loads
- ✓ Status badges and priority indicators are visually distinct

### Launch Configuration (`.vscode/launch.json`)
- ✓ File is valid JSON (no comments, proper syntax)
- ✓ Includes a configuration with `"name": "Run Project Pulse Dashboard"`
- ✓ Configures server with deterministic port (e.g., 8000)
- ✓ Sets `cwd` to `${workspaceFolder}/app`
- ✓ Opens `index.html` automatically (not a directory listing)
- ✓ Clicking **Run** in VS Code starts the server and opens the dashboard in a browser

### Integration
- ✓ All four files exist in their assigned locations
- ✓ Dashboard displays on launch without manual steps
- ✓ Project cards are visible, readable, and styled
- ✓ No broken image references or missing files

## Open Questions

1. **Server technology**: Should the launch config use Python's `http.server` or Node.js `http-server`? (Recommendation: Python if already available in the Codespace; Node.js if http-server is pre-installed.)

2. **JSON loading strategy**: Should `project-data.json` be fetched via `fetch()` API or embedded in the HTML? (Recommendation: Use `fetch()` to keep concerns separated and match modern web practices.)

3. **Client-side rendering vs. pre-rendering**: Should the JavaScript render cards dynamically, or should cards be pre-rendered in HTML? (Recommendation: Dynamic rendering via JavaScript for flexibility and to demonstrate basic JavaScript skills.)

4. **CSS framework or custom**: Should CSS be hand-written or use a framework like Tailwind or Bootstrap? (Recommendation: Hand-written CSS for learning purposes; keep it simple and demonstrable.)

5. **Project card detail level**: Should cards include additional details like start date, end date, or team size, or stick to the brief fields? (Recommendation: Stick to brief fields to keep scope manageable; additional fields can be added later.)

6. **Status values**: What are the valid values for `status`? (e.g., "Active", "At Risk", "Blocked", "Completed") (Recommendation: Use clear, universally understood statuses like "Active", "At Risk", "Blocked", "Paused".)

7. **Priority values**: What are the valid values for `priority`? (e.g., "High", "Medium", "Low") (Recommendation: Use clear levels; consider three-tier system for simplicity.)

8. **Mobile-first or desktop-first CSS**: Should styling prioritize mobile or desktop experience? (Recommendation: Mobile-first approach (start with mobile styles, then enhance for larger screens) is modern best practice.)