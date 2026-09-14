# Technical Requirements Document: Occasion Guide

**Status:** MVP direction 1.0
**Companion:** [PRD](PRD.md)
**Implementation posture:** static HTML/CSS with minimal JavaScript; no backend in the first release.

## 1. Technical approach

Build a small, deploy-anywhere static site. The first version should be understandable and editable by a person who can open an HTML file. Keep content close to the markup until the editorial template has been tested in practice.

```text
Reader
  -> occasion-guide/index.html
  -> embedded guide catalogue and lightweight browser filtering
```

No framework, build pipeline, database, authentication, API, CMS, or runtime service is required for the MVP.

## 2. Repository layout

```text
occasion-guide/
  index.html       # public prototype and guide catalogue
  PRD.md           # product scope and editorial direction
  TRD.md           # implementation and acceptance requirements
  README.md        # run and extend instructions
```

If the page later needs a larger catalogue, split content into static HTML pages or JSON generated during a build. Do not introduce a framework until the content volume or publishing workflow proves that it is necessary.

## 3. Page requirements

- Use semantic HTML landmarks: `header`, `nav`, `main`, `section`, `article`, and `footer`.
- Provide one clear `h1`; sections use a logical heading hierarchy.
- Include a skip link, visible focus states, keyboard-operable controls, and labelled search/filter controls.
- Use explicit links with `index.html` or `.html` paths so local file previews do not depend on directory-index behaviour.
- Keep the main reading column comfortable for long-form text and avoid dense walls of copy.
- Use the Cimulink VSL visual baseline: Manrope body text, Roboto Slab display text, DM Mono utility labels, and the established pine/paper/moss/sand/clay palette.
- Use CSS custom properties, grid/flex layout, and a mobile breakpoint. Avoid external JavaScript dependencies.
- Use progressive enhancement: without JavaScript, all guide cards and sections remain readable; with JavaScript, search and filters refine the visible cards.
- Use `aria-live` for the filtered-result count and do not hide content solely through inaccessible visual tricks.

## 4. Guide data contract

Each guide card/section must provide:

```text
title
alternate names (optional)
guide type
region/tradition (when relevant)
summary
why people observe it
before checklist
on-the-day checklist
after checklist
variation note
questions to confirm locally
safety/accessibility note
sources
review date
```

The HTML `data-search`, `data-type`, and `data-region` attributes are the MVP search index. Keep them aligned with the visible content.

## 5. Minimal interaction contract

- Search matches title, alternate names, summary, region, and visible keywords.
- Type filters are additive with search and include an “All guides” state.
- Empty results show a helpful message and a way to clear the filter.
- Navigation anchors move to the relevant section and remain usable without JavaScript.
- The correction link uses a placeholder email address until the product owner supplies the final editorial contact.

## 6. Security and privacy

- No user data is collected by the MVP.
- No comments, uploads, sign-in, tracking, or third-party analytics are included.
- External source links use normal HTTPS links and open in a new tab with `rel="noreferrer"`.
- Do not embed third-party widgets or user-generated HTML.

## 7. Acceptance checks

- Open `index.html` directly and verify that the full catalogue is readable.
- Serve the folder over a simple local HTTP server and verify the page returns 200.
- Search and type filters update the visible result count and work with keyboard input.
- Verify layout at desktop and 320 px mobile width.
- Verify focus visibility, heading order, link purpose, colour contrast, and reduced-motion behaviour.
- Run an HTML validator if available; report visual/browser checks separately from source checks.

## 8. Upgrade path after validation

Only after readers validate the template:

1. Move guides into Markdown/MDX or a small content collection.
2. Add generated individual guide URLs and local search indexing.
3. Add a CMS only when non-technical editorial publishing is a real bottleneck.
4. Add authentication and pre-moderated contributions as a separate security-reviewed milestone.
5. Add paid planning or partner features only with explicit editorial/commercial separation.
