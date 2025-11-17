# Copilot Instructions for CV_Template_Sergio_Torres

## Project Overview
A **React.js-based CV template** deployed via Netlify. This is a single-page application (SPA) that serves as a portfolio/resume website. The project uses Create React App (CRA) conventions with inline styles and minimal external styling.

**Key URLs:**
- Live deployment: https://cvte.netlify.app/
- Repository: https://github.com/QuimicoProgramador/CV_Template_Sergio_Torres

---

## Architecture & Structure

### Core Design
- **Single component model**: All content lives in `src/App.js`—no nested component architecture
- **Styling approach**: Inline styles via JavaScript objects (no CSS modules or CSS-in-JS libraries)
- **Build system**: Create React App v5 with react-scripts
- **Deployment**: Netlify with automatic builds on push to `main` branch

### File Organization
```
cv_sergio/                    # Main React app (build root)
├── src/
│   ├── App.js               # Main CV component (edit this to customize content)
│   ├── App.css              # Unused legacy styles
│   ├── index.css            # Global styles
│   ├── index.js             # React entry point
│   └── ...test.js           # Test files
├── public/
│   ├── index.html           # HTML shell
│   └── manifest.json        # PWA metadata
└── package.json             # Dependencies & scripts
netlify.toml                  # Netlify build config (base="cv_sergio")
```

---

## Styling Convention

**Important**: This project uses **inline styles only**. Do NOT add external CSS files or CSS imports unless modifying the template architecture.

### Pattern in `App.js`:
```javascript
const containerStyle = {
  maxWidth: "900px",
  margin: "40px auto",
  padding: "20px",
  fontFamily: "Arial, sans-serif"
};

return <div style={containerStyle}>...</div>;
```

**When updating styles**:
- Define styles as JavaScript objects above the return statement
- Use camelCase for CSS properties (e.g., `paddingBottom`, `marginTop`)
- Pass styles via `style={objectName}` attribute
- Keep colors, spacing, and typography consistent with existing styles

---

## Content Editing Pattern

The entire CV content is **template-based** with fill-in-the-blank sections marked by `{/* RELLENAR: ... */}` comments in `App.js`.

### Sections structure (in order):
1. **Header** - Name, title, contact info
2. **Resumen Profesional** - Professional summary
3. **Experiencia Laboral** - Work experience (duplicate `<article>` blocks for multiple jobs)
4. **Habilidades** - Skills categorized by domain
5. **Educación** - Education entries (duplicate `<article>` blocks for multiple degrees)

**Key pattern**: Comments like `{/* RELLENAR: Tu Nombre */}` indicate where content should be replaced. Keep comment structure intact for future users of this template.

---

## Development Workflow

### Local Setup
```bash
cd cv_sergio
npm install
npm start
```
The app runs at `http://localhost:3000` with hot-reload enabled.

### Build & Deployment
```bash
npm run build              # Creates production build in cv_sergio/build/
```

**Deployment is automatic**: Any push to `main` triggers Netlify build via the `netlify.toml` configuration:
```toml
[build]
  command = "npm run build"
  publish = "build/"
  base = "cv_sergio"
```

The `base = "cv_sergio"` setting tells Netlify to work from the React app directory.

### Testing
```bash
npm test                   # Run Jest/React Testing Library tests
```

---

## Dependencies & Ecosystem

| Package | Version | Purpose |
|---------|---------|---------|
| `react` | ^19.2.0 | UI framework |
| `react-dom` | ^19.2.0 | DOM rendering |
| `react-scripts` | 5.0.1 | CRA build tooling |
| `@testing-library/react` | ^16.3.0 | Component testing |

**Dev tools**: ESLint (extends `react-app` config), Prettier (for formatting), no custom webpack config.

---

## Common Tasks

### Task: Update CV Content
1. Open `src/App.js`
2. Find the `{/* RELLENAR: ... */}` comment for the section to edit
3. Replace placeholder text directly (keep comment structure)
4. Test with `npm start` (hot-reload shows changes immediately)

### Task: Modify Styling
1. Open `src/App.js`
2. Edit the style object (e.g., `containerStyle`, `sectionTitleStyle`)
3. Use inline style pattern consistently
4. All styles must be JavaScript objects in the component file

### Task: Add New Sections
1. Follow the existing `<section>` structure in App.js
2. Create new style object at top of component
3. Use same semantic HTML tags (h2, p, article, ul, li)
4. Keep inline styles consistent with existing theme

### Task: Deploy Changes
- Push to `main` branch → Netlify auto-deploys within 1-2 minutes
- Monitor at netlify.app dashboard or check site at https://cvte.netlify.app/

---

## Important Constraints & Patterns

- **No external components**: This is intentionally a single-component template
- **No state management**: Component is purely presentational (no useState, useEffect)
- **No routing**: Single-page, static content only
- **CSS-in-JS inline only**: No CSS modules, Tailwind, or styled-components
- **Spanish language convention**: Comments and default text are in Spanish

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| `npm start` fails with command not found | Ensure Node.js is installed; run from `cv_sergio/` directory |
| Build fails on Netlify | Check `netlify.toml` `base = "cv_sergio"` setting; verify `npm run build` works locally |
| Styles not applying | Confirm using inline styles as JavaScript objects; check browser DevTools for style precedence |
| Hot-reload not working | Restart dev server with `npm start` after file changes |

---

## Quick Reference Commands

```bash
npm install              # Install dependencies (run once after clone)
npm start                # Local dev server at localhost:3000
npm run build            # Production build (outputs to build/)
npm test                 # Run tests in watch mode
npm run eject            # ⚠️ One-way CRA eject (avoid unless necessary)
```
