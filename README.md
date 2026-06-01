# Portfolio Website

Personal engineering portfolio — built with plain HTML and Tailwind CSS.

## Stack

- HTML5 + Tailwind CSS (Play CDN) — no build step
- Vanilla JavaScript (scroll spy only)

## Local development

Open `index.html` directly in a browser. No server needed.

## Deployment (GitHub Pages)

### Option A — Personal site (`yourusername.github.io`)

1. Create a GitHub repo named exactly `yourusername.github.io`
2. Push this repo to `main`:
   ```bash
   git remote add origin https://github.com/yourusername/yourusername.github.io.git
   git push -u origin main
   ```
3. GitHub Pages auto-deploys. Live at `https://yourusername.github.io` within ~1 minute.

### Option B — Project page (`yourusername.github.io/portfolio`)

1. Create any GitHub repo (e.g., `portfolio`)
2. Push to `main`
3. Go to repo **Settings → Pages → Source → Deploy from branch → main / root**
4. Live at `https://yourusername.github.io/portfolio`

## Customisation

- Edit `index.html` directly — all content and styles are inline
- Add project cards by duplicating the `<article>` block in the Projects section
- Add experience entries by duplicating the timeline `<div class="relative pl-12">` block
- Add skill badges by duplicating `<span>` elements in the Skills section

## Personalising

Replace these placeholders in `index.html`:

| Placeholder | Replace with |
|-------------|-------------|
| `Your Name` | Your full name |
| `Software Engineer` | Your actual title |
| `your.email@example.com` | Your email address |
| `yourprofile` (LinkedIn) | Your LinkedIn handle |
| `yourusername` (GitHub) | Your GitHub username |
| Project names/descriptions/URLs | Your actual projects |
| Company names, roles, dates | Your real work history |
| Skills badges | Your actual skills |

Also add:
- `assets/profile.jpg` — your headshot (square crop, min 300×300px)
- `assets/resume.pdf` — your resume PDF
- `assets/projects/project1.png`, `project2.png`, `project3.png` — project screenshots
