# Academic Website Maintenance & Publishing Manual
**Owner:** Uday Shankar Roy  
**Live Website:** [https://udayusr.github.io/](https://udayusr.github.io/)  
**GitHub Repository:** [https://github.com/UdayUSR/udayusr.github.io](https://github.com/UdayUSR/udayusr.github.io)  
**Deployment Branch:** `master` (Automated via GitHub Actions)

---

## 1. Quick Start: How to Edit and Publish in VS Code

### Step 1: Open the Project in VS Code
1. Open VS Code.
2. Go to **File &rarr; Open Folder...** and select `E:\Projects\UdayUSR`.

### Step 2: Make Your Edits
Edit any file described in the **File Roadmap** below and save your changes (`Ctrl + S`).

### Step 3: Make Changes Live on the Website
Choose either **Terminal** (recommended) or the **VS Code GUI**:

#### Method A: Using VS Code Integrated Terminal (Fastest)
1. Open the terminal inside VS Code by pressing **`Ctrl + ` `** (backtick) or selecting **Terminal &rarr; New Terminal** from the top menu.
2. Run these commands:
   ```bash
   git status
   git add .
   git commit -m "Update publication links and bio"
   git push origin master
   ```

#### Method B: Using VS Code Source Control GUI
1. Click the **Source Control** icon on the left sidebar (or press `Ctrl + Shift + G`).
2. Review your modified files under **Changes**.
3. Click the **`+`** icon next to the word *Changes* to stage all edits.
4. Type a short description in the message box above (e.g. `Update publications`).
5. Click the blue **Commit** button (or press `Ctrl + Enter`).
6. Click the blue **Sync Changes** button (or the `...` menu &rarr; **Push**).

### Step 4: Verification
- GitHub automatically triggers a build via **GitHub Actions**.
- It takes **30–60 seconds** to go live.
- Check build progress at: [https://github.com/UdayUSR/udayusr.github.io/actions](https://github.com/UdayUSR/udayusr.github.io/actions)
- Once complete, open [https://udayusr.github.io/](https://udayusr.github.io/). If changes don't show immediately, press **`Ctrl + F5`** (hard refresh) to clear the browser cache.

---

## 2. File Roadmap: Where to Edit What

| What you want to edit | Exact File / Folder | Details |
| :--- | :--- | :--- |
| **Homepage Bio & Research Interests** | `_pages/about.md` | Top introductory paragraph, bulleted interests, and Recent News items. |
| **Publications & Preprints** | `_publications/` | Each paper has its own markdown (`.md`) file. Automatically feeds Homepage, Publications page, and CV. |
| **CV Content (Education, Jobs, etc.)** | `_pages/cv.md` | Degrees, GPA, work experience, IELTS scores, projects. |
| **CV PDF Download File** | `files/Uday_Shankar_Roy_CV.pdf` | Replace this file with your new PDF export (keep filename identical). |
| **Personal Bio, Links, Scholar** | `_config.yml` | Author metadata (`bio`, `googlescholar`, `github`, `linkedin`, `email`). |
| **Blog Posts** | `_posts/` | Markdown files named in the format `YYYY-MM-DD-title.md`. |
| **Navigation Menu (Tabs)** | `_data/navigation.yml` | Top header links (`Home`, `Publications`, `Blog`, `CV`). |
| **Profile Photo** | `images/profilepic_uday.jpg` | Replace image file or change filename in `_config.yml`. |

---

## 3. Publication Management Guide

Each publication is stored as a Markdown file in the `_publications/` directory:
- `_publications/2026-04-15-skin-lesion-hair-segmentation.md`
- `_publications/2026-03-10-frequency-domain-ai-detection.md`
- `_publications/2026-01-15-shortcut-learning-iot-intrusion-detection.md`
- `_publications/2026-02-01-prompt-triage-llm-defense.md`

### Publication Chronology Rule
All publication lists (Homepage, `/publications/`, and `/cv/`) sort automatically in **descending chronological order based on the `date:` field**.
- To move a paper higher in the list, give it a more recent `date: YYYY-MM-DD`.
- To move a paper lower, assign an earlier date.

### How Paper Titles Link
- If a paper has a `doi:`, clicking its title automatically opens the **official DOI link** in a new tab.
- If it has an `arxiv:` link but no DOI, clicking its title opens the **arXiv preprint** in a new tab.
- If it has neither (e.g., *PromptTriage* while under review), clicking the title opens the internal GitHub Pages details page with the abstract.

### Publication File Template
Copy and adjust this template when adding a new paper or updating an existing one:

```markdown
---
title: "Paper Title Goes Here"
collection: publications
category: conferences       # Options: conferences, manuscripts, under_review
permalink: /publication/unique-paper-slug
status: "Accepted & Published" # Options: "Accepted", "Accepted & Published", "Under Review", or leave blank
authors: "<strong>Uday Shankar Roy</strong>, Co-Author Name"
date: 2026-05-01             # Controls chronological sorting
venue: "IEEE SHORT_NAME 2026" # Short name shown on Homepage and /publications/ cards
full_venue: "2026 IEEE Full International Conference Name (ACRONYM)" # Used on CV (/cv/)
doi: "https://doi.org/10.xxxx/xxxxxxx"       # Official publisher DOI link (if published)
arxiv: "https://arxiv.org/abs/26xx.xxxxx"    # arXiv abstract URL (if preprint available)
paperurl: "https://arxiv.org/pdf/26xx.xxxxx" # Direct PDF download link
citation: "Roy, U. S., & Co-Author. (2026). Paper Title. In Full Venue Name. DOI/arXiv."
excerpt: "1-2 sentence concise summary shown on publication cards."
---

## Abstract
Paste the full paper abstract here. Markdown formatting and bold text are supported.

**Venue:** Full Conference Name  
**Status:** Accepted / Published / Under Review  
**Official DOI:** [Link Text](https://doi.org/...)
```

---

## 4. Common Recipes

### Recipe 1: Adding a DOI when an Accepted Paper is Published
Suppose IEEE publishes the OMLET paper and assigns a DOI:
1. Open `_publications/2026-03-10-frequency-domain-ai-detection.md`.
2. Add or update the `doi:` line in the frontmatter:
   ```yaml
   status: "Accepted & Published"
   doi: "https://doi.org/10.1109/OMLET.2026.xxxxxxx"
   ```
3. Update `citation:` to include the DOI.
4. Save, commit, and push. The paper title will now automatically route to the IEEE DOI link, and a `[DOI]` badge will appear on cards and CV.

---

### Recipe 2: Adding a New Entry to Recent News
1. Open `_pages/about.md`.
2. Locate the `<div class="news-list">` section (around line 28).
3. Add a new item at the top of the list:
   ```html
   <div style="display: flex; gap: 16px; margin-bottom: 12px; align-items: baseline;">
     <span style="display: inline-block; min-width: 82px; text-align: center; padding: 2px 8px; font-size: 0.82em; font-weight: 700; border-radius: 4px; background: rgba(125, 125, 125, 0.12); color: var(--global-text-color); border: 1px solid var(--global-border-color); flex-shrink: 0;">May 2026</span>
     <span style="color: var(--global-text-color); line-height: 1.5;">Our paper was accepted at <strong>Conference Name</strong>!</span>
   </div>
   ```
4. Save, commit, and push.

---

### Recipe 3: Updating Your CV PDF
1. Export your updated CV from Word/LaTeX to PDF.
2. Name the exported PDF file exactly: `Uday_Shankar_Roy_CV.pdf`.
3. Copy/overwrite it into `E:\Projects\UdayUSR\files\Uday_Shankar_Roy_CV.pdf`.
4. (Optional) If you also want to update text entries (Education, Work Experience), edit `_pages/cv.md`.
5. Run:
   ```bash
   git add files/Uday_Shankar_Roy_CV.pdf _pages/cv.md
   git commit -m "Update CV PDF and experience"
   git push origin master
   ```

---

### Recipe 4: Writing a New Blog Post
1. Inside `_posts/`, create a new file named with today's date, e.g.:
   `_posts/2026-10-01-my-new-research-note.md`
2. Add the header:
   ```markdown
   ---
   title: "My Research Note Title"
   date: 2026-10-01
   permalink: /blog/2026/10/my-new-research-note/
   tags:
     - Machine Learning
     - Security
   ---

   Your blog content here in markdown...
   ```
3. Save, commit, and push. It will automatically list under the `/blog/` page.

---

## 5. Important Design & Configuration Notes

- **Default Desktop Scale:** The site uses a `zoom: 0.9` default scale for desktop viewports (`_sass/layout/_base.scss`), providing a sleek, compact layout.
- **Dark/Light Theme Toggle:** The site uses the top-right toggle button (`fa-sun` / `fa-moon`) configured in `_includes/head.html` and `_sass/_themes.scss`.
- **Conference Naming Convention:**
  - `venue:` Used for cards on Homepage and `/publications/` (e.g. `IEEE QPAIN 2026`).
  - `full_venue:` Used for the formal CV list on `/cv/` (e.g. `2026 IEEE 2nd International Conference on Quantum Photonics, Artificial Intelligence & Networking (QPAIN)`).
- **Git Branch Rule:** Always commit and push directly to the `master` branch. GitHub Actions is configured to trigger on pushes to `master`.
