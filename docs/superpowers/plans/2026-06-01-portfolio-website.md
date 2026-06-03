# Portfolio Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single-file professional engineering portfolio website deployed to GitHub Pages.

**Architecture:** One `index.html` containing all five sections (About, Projects, Skills, Experience, Contact) with a fixed nav and smooth scroll. Tailwind CSS Play CDN handles all styling — no build step. A 15-line vanilla JS `IntersectionObserver` handles active nav highlighting.

**Tech Stack:** HTML5, Tailwind CSS (Play CDN v3), Vanilla JavaScript, GitHub Pages

---

## File Map

| File | Responsibility |
|------|---------------|
| `index.html` | Entire site — all sections, nav, footer, JS |
| `assets/profile.jpg` | Profile photo (user supplies) |
| `assets/projects/` | Project screenshots (user supplies) |
| `README.md` | GitHub Pages deployment instructions |

---

## Task 1: Project scaffold and base HTML

**Files:**
- Create: `index.html`
- Create: `assets/projects/.gitkeep`

- [ ] **Step 1: Create the assets directories**

```
portfolio/
├── assets/
│   └── projects/
```

In your terminal (or file explorer), create the folder structure:
```bash
mkdir -p assets/projects
touch assets/projects/.gitkeep
```

- [ ] **Step 2: Create `index.html` with base structure**

Create `index.html` with the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="Software Engineer portfolio — projects, skills, and experience." />
  <title>Your Name — Software Engineer</title>

  <!-- Tailwind CSS Play CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            navy: {
              DEFAULT: '#1e3a5f',
              light:   '#2a5298',
              dark:    '#152a47',
            }
          },
          fontFamily: {
            sans: [
              '-apple-system', 'BlinkMacSystemFont', '"Segoe UI"',
              'Roboto', 'Oxygen', 'Ubuntu', 'Cantarell', 'sans-serif'
            ],
          }
        }
      }
    }
  </script>

  <style>
    html { scroll-behavior: smooth; }
    /* Offset scroll target so fixed nav doesn't cover section headings */
    section { scroll-margin-top: 4rem; }
    /* Active nav link style applied by JS */
    nav a.active { color: #93c5fd; /* Tailwind blue-300 */ }
  </style>
</head>
<body class="font-sans text-slate-700 bg-white">

  <!-- NAV placeholder -->
  <!-- MAIN placeholder -->
  <!-- FOOTER placeholder -->

</body>
</html>
```

- [ ] **Step 3: Verify scaffold in browser**

Open `index.html` in your browser (double-click the file or drag into Chrome/Edge).
Expected: blank white page, no console errors, page title shows "Your Name — Software Engineer".

- [ ] **Step 4: Commit**

```bash
git init          # if not already a git repo
git add index.html assets/
git commit -m "chore: project scaffold with Tailwind CDN"
```

---

## Task 2: Fixed navigation bar

**Files:**
- Modify: `index.html` — replace `<!-- NAV placeholder -->`

- [ ] **Step 1: Replace the NAV placeholder with this block**

```html
  <!-- ===== NAVIGATION ===== -->
  <header class="fixed top-0 left-0 right-0 z-50 bg-navy shadow-md">
    <nav class="max-w-6xl mx-auto px-6 py-4 flex items-center justify-between" aria-label="Main navigation">

      <!-- Logo / Name -->
      <a href="#about" class="text-white font-bold text-xl tracking-tight hover:text-blue-300 transition-colors">
        Your Name
      </a>

      <!-- Desktop nav links -->
      <ul class="hidden md:flex gap-8 text-sm font-medium text-slate-300">
        <li><a href="#about"      class="hover:text-white transition-colors">About</a></li>
        <li><a href="#projects"   class="hover:text-white transition-colors">Projects</a></li>
        <li><a href="#skills"     class="hover:text-white transition-colors">Skills</a></li>
        <li><a href="#experience" class="hover:text-white transition-colors">Experience</a></li>
        <li><a href="#contact"    class="hover:text-white transition-colors">Contact</a></li>
      </ul>

      <!-- Mobile: hamburger (pure CSS checkbox toggle) -->
      <div class="md:hidden relative">
        <input type="checkbox" id="menu-toggle" class="peer sr-only" aria-label="Toggle navigation menu" />
        <label for="menu-toggle" class="cursor-pointer text-white select-none text-2xl" aria-hidden="true">&#9776;</label>

        <!-- Mobile dropdown -->
        <ul class="hidden peer-checked:flex flex-col absolute right-0 top-10 bg-navy-dark w-48 rounded-lg shadow-xl
                   text-slate-200 text-sm font-medium py-2 z-50">
          <li><a href="#about"      onclick="document.getElementById('menu-toggle').checked=false"
                 class="block px-4 py-2 hover:bg-navy-light transition-colors">About</a></li>
          <li><a href="#projects"   onclick="document.getElementById('menu-toggle').checked=false"
                 class="block px-4 py-2 hover:bg-navy-light transition-colors">Projects</a></li>
          <li><a href="#skills"     onclick="document.getElementById('menu-toggle').checked=false"
                 class="block px-4 py-2 hover:bg-navy-light transition-colors">Skills</a></li>
          <li><a href="#experience" onclick="document.getElementById('menu-toggle').checked=false"
                 class="block px-4 py-2 hover:bg-navy-light transition-colors">Experience</a></li>
          <li><a href="#contact"    onclick="document.getElementById('menu-toggle').checked=false"
                 class="block px-4 py-2 hover:bg-navy-light transition-colors">Contact</a></li>
        </ul>
      </div>

    </nav>
  </header>

  <!-- Push content below fixed nav -->
  <div class="h-16"></div>
```

- [ ] **Step 2: Verify nav in browser**

Refresh `index.html`.
Expected: navy bar fixed at top with "Your Name" on the left. On desktop: nav links on the right. Narrow window to mobile width: hamburger ☰ appears; clicking it opens dropdown, clicking a link closes it.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: fixed navigation bar with mobile hamburger"
```

---

## Task 3: Hero / About section

**Files:**
- Modify: `index.html` — replace `<!-- MAIN placeholder -->` with `<main>` + About section

- [ ] **Step 1: Replace `<!-- MAIN placeholder -->` with this block**

```html
  <!-- ===== MAIN CONTENT ===== -->
  <main>

    <!-- ===== ABOUT ===== -->
    <section id="about" class="bg-white py-20 px-6">
      <div class="max-w-6xl mx-auto flex flex-col-reverse md:flex-row items-center gap-12">

        <!-- Text -->
        <div class="flex-1">
          <p class="text-blue-600 font-semibold text-sm uppercase tracking-widest mb-2">Welcome</p>
          <h1 class="text-4xl md:text-5xl font-bold text-navy mb-4 leading-tight">
            Hi, I'm <span class="text-blue-600">Your Name</span>
          </h1>
          <p class="text-xl text-slate-500 font-medium mb-4">Software Engineer</p>
          <p class="text-slate-600 text-lg leading-relaxed mb-8">
            I build reliable, scalable software with a focus on clean architecture and
            pragmatic engineering. With X years of experience across Y and Z, I enjoy
            solving hard problems and shipping products that matter.
          </p>
          <div class="flex flex-wrap gap-4">
            <a href="#projects"
               class="bg-navy text-white px-6 py-3 rounded-lg font-semibold hover:bg-navy-light transition-colors">
              View My Work
            </a>
            <a href="assets/resume.pdf" target="_blank" rel="noopener"
               class="border-2 border-navy text-navy px-6 py-3 rounded-lg font-semibold hover:bg-navy hover:text-white transition-colors">
              Download Resume
            </a>
          </div>
        </div>

        <!-- Photo -->
        <div class="flex-shrink-0">
          <img src="assets/profile.jpg"
               alt="Profile photo of Your Name"
               class="w-56 h-56 md:w-72 md:h-72 rounded-full object-cover shadow-xl border-4 border-slate-100" />
        </div>

      </div>
    </section>

    <!-- Projects, Skills, Experience, Contact sections go here -->

  </main>
```

- [ ] **Step 2: Add a placeholder profile image**

Add any square `.jpg` as `assets/profile.jpg` temporarily. You can replace it with your real photo later.
If you have no image yet, the `<img>` will show as a broken image — that's fine for now.

- [ ] **Step 3: Verify About section in browser**

Refresh `index.html`.
Expected: Hero section with name, title, bio paragraph, two buttons side-by-side. On mobile: photo stacks above text.

- [ ] **Step 4: Commit**

```bash
git add index.html assets/profile.jpg
git commit -m "feat: hero/about section"
```

---

## Task 4: Projects section

**Files:**
- Modify: `index.html` — replace `<!-- Projects, Skills, Experience, Contact sections go here -->`

- [ ] **Step 1: Insert the Projects section**

Replace the comment with the Projects section (keep the comment's position for later tasks):

```html
    <!-- ===== PROJECTS ===== -->
    <section id="projects" class="bg-slate-50 py-20 px-6">
      <div class="max-w-6xl mx-auto">

        <div class="text-center mb-12">
          <p class="text-blue-600 font-semibold text-sm uppercase tracking-widest mb-2">My Work</p>
          <h2 class="text-3xl md:text-4xl font-bold text-navy">Projects</h2>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">

          <!-- Project Card -->
          <article class="bg-white rounded-xl shadow-sm hover:shadow-lg transition-shadow border border-slate-100 flex flex-col">
            <img src="assets/projects/project1.png"
                 alt="Screenshot of Project One"
                 class="w-full h-48 object-cover rounded-t-xl bg-slate-200" />
            <div class="p-6 flex flex-col flex-1">
              <h3 class="text-lg font-bold text-navy mb-2">Project One</h3>
              <p class="text-slate-600 text-sm mb-4 flex-1">
                A brief one-line description of what this project does and the problem it solves.
              </p>
              <!-- Tech tags -->
              <div class="flex flex-wrap gap-2 mb-4">
                <span class="bg-blue-50 text-blue-700 text-xs font-medium px-2 py-1 rounded">Python</span>
                <span class="bg-blue-50 text-blue-700 text-xs font-medium px-2 py-1 rounded">FastAPI</span>
                <span class="bg-blue-50 text-blue-700 text-xs font-medium px-2 py-1 rounded">PostgreSQL</span>
              </div>
              <!-- Links -->
              <div class="flex gap-4 text-sm font-medium">
                <a href="https://github.com/yourusername/project-one" target="_blank" rel="noopener"
                   class="text-navy hover:text-blue-600 transition-colors">GitHub →</a>
                <a href="https://project-one-demo.example.com" target="_blank" rel="noopener"
                   class="text-navy hover:text-blue-600 transition-colors">Live Demo →</a>
              </div>
            </div>
          </article>

          <!-- Project Card -->
          <article class="bg-white rounded-xl shadow-sm hover:shadow-lg transition-shadow border border-slate-100 flex flex-col">
            <img src="assets/projects/project2.png"
                 alt="Screenshot of Project Two"
                 class="w-full h-48 object-cover rounded-t-xl bg-slate-200" />
            <div class="p-6 flex flex-col flex-1">
              <h3 class="text-lg font-bold text-navy mb-2">Project Two</h3>
              <p class="text-slate-600 text-sm mb-4 flex-1">
                A brief one-line description of what this project does and the problem it solves.
              </p>
              <div class="flex flex-wrap gap-2 mb-4">
                <span class="bg-blue-50 text-blue-700 text-xs font-medium px-2 py-1 rounded">React</span>
                <span class="bg-blue-50 text-blue-700 text-xs font-medium px-2 py-1 rounded">TypeScript</span>
                <span class="bg-blue-50 text-blue-700 text-xs font-medium px-2 py-1 rounded">Node.js</span>
              </div>
              <div class="flex gap-4 text-sm font-medium">
                <a href="https://github.com/yourusername/project-two" target="_blank" rel="noopener"
                   class="text-navy hover:text-blue-600 transition-colors">GitHub →</a>
                <a href="https://project-two-demo.example.com" target="_blank" rel="noopener"
                   class="text-navy hover:text-blue-600 transition-colors">Live Demo →</a>
              </div>
            </div>
          </article>

          <!-- Project Card -->
          <article class="bg-white rounded-xl shadow-sm hover:shadow-lg transition-shadow border border-slate-100 flex flex-col">
            <img src="assets/projects/project3.png"
                 alt="Screenshot of Project Three"
                 class="w-full h-48 object-cover rounded-t-xl bg-slate-200" />
            <div class="p-6 flex flex-col flex-1">
              <h3 class="text-lg font-bold text-navy mb-2">Project Three</h3>
              <p class="text-slate-600 text-sm mb-4 flex-1">
                A brief one-line description of what this project does and the problem it solves.
              </p>
              <div class="flex flex-wrap gap-2 mb-4">
                <span class="bg-blue-50 text-blue-700 text-xs font-medium px-2 py-1 rounded">Java</span>
                <span class="bg-blue-50 text-blue-700 text-xs font-medium px-2 py-1 rounded">Spring Boot</span>
                <span class="bg-blue-50 text-blue-700 text-xs font-medium px-2 py-1 rounded">Docker</span>
              </div>
              <div class="flex gap-4 text-sm font-medium">
                <a href="https://github.com/yourusername/project-three" target="_blank" rel="noopener"
                   class="text-navy hover:text-blue-600 transition-colors">GitHub →</a>
                <a href="https://project-three-demo.example.com" target="_blank" rel="noopener"
                   class="text-navy hover:text-blue-600 transition-colors">Live Demo →</a>
              </div>
            </div>
          </article>

        </div>
      </div>
    </section>

    <!-- Skills, Experience, Contact sections go here -->
```

- [ ] **Step 2: Verify Projects section in browser**

Refresh `index.html` and scroll to Projects.
Expected: Light gray background, 3 project cards in a row on desktop (stacked on mobile). Cards have a shadow on hover. Image areas show gray placeholder boxes (no real screenshots yet — that's fine).

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: projects section with card grid"
```

---

## Task 5: Skills section

**Files:**
- Modify: `index.html` — replace `<!-- Skills, Experience, Contact sections go here -->`

- [ ] **Step 1: Insert the Skills section**

```html
    <!-- ===== SKILLS ===== -->
    <section id="skills" class="bg-white py-20 px-6">
      <div class="max-w-6xl mx-auto">

        <div class="text-center mb-12">
          <p class="text-blue-600 font-semibold text-sm uppercase tracking-widest mb-2">What I Know</p>
          <h2 class="text-3xl md:text-4xl font-bold text-navy">Skills</h2>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">

          <!-- Category -->
          <div>
            <h3 class="text-navy font-bold text-sm uppercase tracking-widest mb-3 border-b-2 border-blue-100 pb-2">
              Languages
            </h3>
            <div class="flex flex-wrap gap-2">
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">Python</span>
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">JavaScript</span>
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">TypeScript</span>
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">Java</span>
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">SQL</span>
            </div>
          </div>

          <!-- Category -->
          <div>
            <h3 class="text-navy font-bold text-sm uppercase tracking-widest mb-3 border-b-2 border-blue-100 pb-2">
              Frameworks
            </h3>
            <div class="flex flex-wrap gap-2">
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">React</span>
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">Node.js</span>
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">FastAPI</span>
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">Spring Boot</span>
            </div>
          </div>

          <!-- Category -->
          <div>
            <h3 class="text-navy font-bold text-sm uppercase tracking-widest mb-3 border-b-2 border-blue-100 pb-2">
              Tools
            </h3>
            <div class="flex flex-wrap gap-2">
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">Git</span>
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">Docker</span>
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">Linux</span>
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">VS Code</span>
            </div>
          </div>

          <!-- Category -->
          <div>
            <h3 class="text-navy font-bold text-sm uppercase tracking-widest mb-3 border-b-2 border-blue-100 pb-2">
              Platforms
            </h3>
            <div class="flex flex-wrap gap-2">
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">AWS</span>
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">GitHub</span>
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">PostgreSQL</span>
              <span class="bg-slate-100 text-slate-700 text-sm px-3 py-1 rounded-full">Redis</span>
            </div>
          </div>

        </div>
      </div>
    </section>

    <!-- Experience, Contact sections go here -->
```

- [ ] **Step 2: Verify Skills section in browser**

Scroll to Skills.
Expected: 4 columns on desktop (2 on tablet, 1 on mobile). Each column has a category label underlined in light blue, with pill-shaped skill badges below.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: skills section with category badges"
```

---

## Task 6: Experience section

**Files:**
- Modify: `index.html` — replace `<!-- Experience, Contact sections go here -->`

- [ ] **Step 1: Insert the Experience section**

```html
    <!-- ===== EXPERIENCE ===== -->
    <section id="experience" class="bg-slate-50 py-20 px-6">
      <div class="max-w-6xl mx-auto">

        <div class="text-center mb-12">
          <p class="text-blue-600 font-semibold text-sm uppercase tracking-widest mb-2">Career</p>
          <h2 class="text-3xl md:text-4xl font-bold text-navy">Experience</h2>
        </div>

        <!-- Timeline -->
        <div class="relative max-w-3xl mx-auto">

          <!-- Vertical line -->
          <div class="absolute left-4 top-0 bottom-0 w-0.5 bg-blue-100"></div>

          <!-- Entry -->
          <div class="relative pl-12 pb-12">
            <!-- Dot -->
            <div class="absolute left-3 top-1 w-3 h-3 rounded-full bg-navy border-2 border-white shadow"></div>

            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-100">
              <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between mb-2">
                <h3 class="text-lg font-bold text-navy">Senior Software Engineer</h3>
                <span class="text-sm text-slate-400 font-medium mt-1 sm:mt-0">Jan 2022 – Present</span>
              </div>
              <p class="text-blue-600 font-semibold text-sm mb-3">Company Name, City</p>
              <ul class="text-slate-600 text-sm space-y-1 list-disc list-inside">
                <li>Led development of X, reducing latency by Y% and improving Z.</li>
                <li>Architected and shipped a new microservice handling N requests/day.</li>
                <li>Mentored a team of 3 junior engineers through design reviews and code reviews.</li>
              </ul>
            </div>
          </div>

          <!-- Entry -->
          <div class="relative pl-12 pb-12">
            <div class="absolute left-3 top-1 w-3 h-3 rounded-full bg-navy border-2 border-white shadow"></div>
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-100">
              <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between mb-2">
                <h3 class="text-lg font-bold text-navy">Software Engineer</h3>
                <span class="text-sm text-slate-400 font-medium mt-1 sm:mt-0">Jun 2019 – Dec 2021</span>
              </div>
              <p class="text-blue-600 font-semibold text-sm mb-3">Previous Company, City</p>
              <ul class="text-slate-600 text-sm space-y-1 list-disc list-inside">
                <li>Built and maintained REST APIs serving over N active users.</li>
                <li>Migrated legacy monolith components to containerised services using Docker.</li>
                <li>Reduced CI pipeline duration from X minutes to Y minutes.</li>
              </ul>
            </div>
          </div>

          <!-- Entry -->
          <div class="relative pl-12">
            <div class="absolute left-3 top-1 w-3 h-3 rounded-full bg-slate-300 border-2 border-white shadow"></div>
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-100">
              <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between mb-2">
                <h3 class="text-lg font-bold text-navy">Software Engineering Intern</h3>
                <span class="text-sm text-slate-400 font-medium mt-1 sm:mt-0">May 2018 – Aug 2018</span>
              </div>
              <p class="text-blue-600 font-semibold text-sm mb-3">Internship Company, City</p>
              <ul class="text-slate-600 text-sm space-y-1 list-disc list-inside">
                <li>Developed a reporting dashboard used daily by the operations team.</li>
                <li>Fixed 12 production bugs and added unit tests to previously untested modules.</li>
              </ul>
            </div>
          </div>

        </div>
      </div>
    </section>

    <!-- Contact section goes here -->
```

- [ ] **Step 2: Verify Experience section in browser**

Scroll to Experience.
Expected: Light gray background. Three cards in a vertical timeline with a thin blue vertical line and navy dots connecting them. Each card shows role, company, date, and bullet points.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: experience section with vertical timeline"
```

---

## Task 7: Contact section and footer

**Files:**
- Modify: `index.html` — replace `<!-- Contact section goes here -->` and `<!-- FOOTER placeholder -->`

- [ ] **Step 1: Insert the Contact section and close `<main>`**

Replace `<!-- Contact section goes here -->` with:

```html
    <!-- ===== CONTACT ===== -->
    <section id="contact" class="bg-navy py-20 px-6">
      <div class="max-w-6xl mx-auto text-center">

        <p class="text-blue-300 font-semibold text-sm uppercase tracking-widest mb-2">Get In Touch</p>
        <h2 class="text-3xl md:text-4xl font-bold text-white mb-4">Contact</h2>
        <p class="text-slate-300 text-lg mb-10 max-w-xl mx-auto">
          I'm open to full-time roles, contract work, and interesting projects.
          Reach out through any of the channels below.
        </p>

        <div class="flex flex-col sm:flex-row items-center justify-center gap-8">

          <!-- Email -->
          <a href="mailto:your.email@example.com"
             class="flex items-center gap-3 text-slate-200 hover:text-white transition-colors group">
            <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 text-blue-300 group-hover:text-white transition-colors"
                 fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round"
                    d="M21.75 6.75v10.5a2.25 2.25 0 01-2.25 2.25H4.5a2.25 2.25 0 01-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0019.5 4.5H4.5a2.25 2.25 0 00-2.25 2.25m19.5 0l-9.75 6.75L2.25 6.75" />
            </svg>
            <span class="font-medium">your.email@example.com</span>
          </a>

          <!-- LinkedIn -->
          <a href="https://linkedin.com/in/yourprofile" target="_blank" rel="noopener"
             class="flex items-center gap-3 text-slate-200 hover:text-white transition-colors group">
            <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 text-blue-300 group-hover:text-white transition-colors"
                 fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path d="M20.447 20.452H17.21v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.988V9h3.109v1.562h.045c.434-.822 1.492-1.689 3.073-1.689 3.286 0 3.893 2.162 3.893 4.976v6.603zM5.337 7.433a1.803 1.803 0 110-3.605 1.803 1.803 0 010 3.605zm1.557 13.019H3.779V9h3.115v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
            </svg>
            <span class="font-medium">linkedin.com/in/yourprofile</span>
          </a>

          <!-- GitHub -->
          <a href="https://github.com/yourusername" target="_blank" rel="noopener"
             class="flex items-center gap-3 text-slate-200 hover:text-white transition-colors group">
            <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 text-blue-300 group-hover:text-white transition-colors"
                 fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/>
            </svg>
            <span class="font-medium">github.com/yourusername</span>
          </a>

        </div>
      </div>
    </section>

  </main>
  <!-- end of main -->
```

- [ ] **Step 2: Replace `<!-- FOOTER placeholder -->` with the footer**

```html
  <!-- ===== FOOTER ===== -->
  <footer class="bg-navy-dark py-6 px-6 text-center">
    <p class="text-slate-400 text-sm">
      &copy; 2026 Your Name &mdash; Built with HTML &amp; Tailwind CSS
    </p>
  </footer>
```

- [ ] **Step 3: Verify Contact and Footer in browser**

Scroll to the bottom.
Expected: Navy background Contact section with three icon+link rows centered. Icons are blue-300, text is light. Footer has a slightly darker navy background with a single copyright line.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: contact section and footer"
```

---

## Task 8: Active nav scroll spy

**Files:**
- Modify: `index.html` — add `<script>` block before `</body>`

- [ ] **Step 1: Add the IntersectionObserver script before `</body>`**

```html
  <script>
    const sections  = document.querySelectorAll('section[id]');
    const navLinks  = document.querySelectorAll('nav a[href^="#"]');

    const observer = new IntersectionObserver(entries => {
      entries.forEach(entry => {
        if (!entry.isIntersecting) return;
        navLinks.forEach(l => l.classList.remove('active'));
        const link = document.querySelector(`nav a[href="#${entry.target.id}"]`);
        if (link) link.classList.add('active');
      });
    }, { rootMargin: '-40% 0px -55% 0px' });

    sections.forEach(s => observer.observe(s));
  </script>
```

The `rootMargin` of `-40% 0px -55% 0px` triggers when a section crosses the upper third of the viewport — this gives clean, predictable highlighting as you scroll.

- [ ] **Step 2: Verify scroll spy in browser**

Open `index.html` and scroll slowly from top to bottom.
Expected: the corresponding nav link (About, Projects, Skills, Experience, Contact) turns blue-300 as each section enters the viewport. Only one link is active at a time.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: active nav highlight via IntersectionObserver"
```

---

## Task 9: Personalise content

**Files:**
- Modify: `index.html` — replace all placeholder text with real content

- [ ] **Step 1: Replace placeholder text throughout `index.html`**

Search for and replace each of the following with your real information:

| Placeholder | Replace with |
|-------------|-------------|
| `Your Name` | Your full name |
| `Software Engineer` | Your actual title |
| `X years of experience across Y and Z` | Your actual experience summary |
| `your.email@example.com` | Your email |
| `yourprofile` (LinkedIn) | Your LinkedIn handle |
| `yourusername` (GitHub) | Your GitHub username |
| `project-one`, `project-two`, `project-three` | Your actual project names, descriptions, tech stacks, URLs |
| Company names, roles, dates in Experience | Your real work history |
| Skills badges | Your actual skills |
| `&copy; 2026` | Current year |

- [ ] **Step 2: Add your profile photo**

Replace `assets/profile.jpg` with your actual headshot (square crop recommended, min 300×300px).

- [ ] **Step 3: Add project screenshots**

Add screenshot images to `assets/projects/`:
- `assets/projects/project1.png`
- `assets/projects/project2.png`
- `assets/projects/project3.png`

If you have no screenshots yet, remove the `<img>` tags from project cards and delete the `rounded-t-xl` class from the card — the card will start with the text directly.

- [ ] **Step 4: Add your resume PDF**

Place your resume at `assets/resume.pdf`. The "Download Resume" button already links to this path.

- [ ] **Step 5: Commit**

```bash
git add index.html assets/
git commit -m "content: add real personal info, projects, and assets"
```

---

## Task 10: README and GitHub Pages deployment

**Files:**
- Create: `README.md`

- [ ] **Step 1: Create `README.md`**

```markdown
# Portfolio Website

Personal engineering portfolio — [yourname.github.io](https://yourusername.github.io)

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
```

- [ ] **Step 2: Commit and push**

```bash
git add README.md
git commit -m "docs: README with deployment instructions"
git push -u origin main
```

- [ ] **Step 3: Verify deployment**

After pushing, go to your GitHub repo → **Settings → Pages**.
Expected: a green banner showing "Your site is live at `https://yourusername.github.io`".
Visit the URL — the full portfolio should appear, identical to your local version.

- [ ] **Step 4: Verify on mobile**

Open the live URL on your phone.
Expected: nav collapses to hamburger, project cards stack to one column, about photo stacks above text, all links work.

---

## Completion Checklist

- [ ] All 5 sections visible and correctly styled
- [ ] Fixed nav with working anchor links
- [ ] Hamburger menu works on mobile
- [ ] Active nav link highlights as you scroll
- [ ] Project cards show hover shadow
- [ ] "Download Resume" links to `assets/resume.pdf`
- [ ] Contact links open correct email/LinkedIn/GitHub
- [ ] Site is live on GitHub Pages
- [ ] Looks correct on mobile (test at 375px width)
