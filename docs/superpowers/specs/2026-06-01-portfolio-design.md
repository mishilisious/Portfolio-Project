# Portfolio Website — Design Spec

**Date:** 2026-06-01  
**Status:** Approved

---

## Purpose

A personal engineering portfolio website to showcase software work to potential employers and clients. Static site deployed to GitHub Pages.

---

## Stack

- **HTML/CSS:** Plain HTML5 with semantic elements
- **Styling:** Tailwind CSS via CDN (no build step)
- **JavaScript:** Minimal vanilla JS (~15 lines for scroll spy)
- **Hosting:** GitHub Pages (push to `main` branch, no CI needed)

---

## File Structure

```
portfolio/
├── index.html          # entire site — all sections in one file
├── assets/
│   ├── profile.jpg     # headshot / profile photo
│   └── projects/       # project screenshots
└── README.md
```

---

## Visual Style

- **Theme:** Professional / corporate
- **Color palette:** Navy primary (`#1e3a5f`), white background, slate-gray body text, blue accent for links and highlights
- **Typography:** System font stack (no external font dependencies)
- **No animations or carousels** — clean, fast, trustworthy

---

## Page Sections

All sections live in `index.html` as stacked full-width blocks with anchor IDs.

### 1. Navigation
- Fixed top navbar
- Anchor links: `#about`, `#projects`, `#skills`, `#experience`, `#contact`
- Collapses to hamburger on mobile (pure CSS)
- Active link highlights on scroll via `IntersectionObserver`

### 2. Hero / About (`#about`)
- Full-width banner
- Name, job title (e.g., "Software Engineer")
- 2–3 sentence bio
- Profile photo (right side on desktop, top on mobile)
- Two CTA buttons: "View My Work" (scroll to #projects) and "Download Resume" (link to PDF)

### 3. Projects (`#projects`)
- Card grid: 3 columns desktop → 1 column mobile
- Each card: project name, 1-line description, tech stack tags, GitHub link, live demo link
- Placeholder for 3–6 projects
- Hover: subtle shadow lift (`hover:shadow-lg`)

### 4. Skills (`#skills`)
- Grid of skill categories: Languages, Frameworks, Tools, etc.
- Individual skill badges per category
- No progress bars (subjective, unprofessional to technical reviewers)

### 5. Experience (`#experience`)
- Vertical timeline layout
- Each entry: company name, role, date range, 2–3 bullet points
- Left-border accent line as visual connector

### 6. Contact (`#contact`)
- Email, LinkedIn, GitHub — icon + link each
- No contact form (avoids backend / third-party dependency)

### 7. Footer
- One line: name + year + "Built with HTML & Tailwind CSS"

---

## Responsiveness

Tailwind responsive prefixes (`sm:`, `md:`, `lg:`) handle all breakpoints. No separate CSS files needed.

---

## Accessibility

- Semantic HTML: `<nav>`, `<main>`, `<section>`, `<footer>`
- `alt` text on all images
- Sufficient color contrast (WCAG AA)

---

## Interactions

| Behaviour | Implementation |
|-----------|---------------|
| Smooth scroll | CSS `scroll-behavior: smooth` |
| Active nav highlight | Vanilla JS `IntersectionObserver` |
| Card hover effect | Tailwind `hover:shadow-lg transition` |

---

## Deployment

- Repo named `<username>.github.io` → `https://<username>.github.io`
- Or any repo with GitHub Pages enabled on `main` → `https://<username>.github.io/<reponame>`
- No build step — push `index.html` and GitHub Pages serves immediately

---

## Out of Scope

- Contact form (requires backend or third-party)
- Dark mode toggle
- Blog / articles
- Animations / scroll effects beyond smooth scroll
