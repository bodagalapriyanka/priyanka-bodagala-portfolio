# Publishing & Maintenance Guide

How to publish this portfolio to GitHub Pages and keep it updated.

---

## 1. Create the GitHub repository

**Recommended repo name:** `priyanka-bodagala-portfolio` (a clean, professional URL slug)
**Repo visibility:** Public

```bash
cd "/Users/priyanka/Desktop/Priyanka's Desktop/Portfolio"

# Initialize git
git init
git branch -M main

# Create a .gitignore so private files stay private
cat > .gitignore <<'EOF'
# Private — do not publish
docs/evidence-index.md
*.private.md
*.draft.md

# OS / editor noise
.DS_Store
Thumbs.db
.idea/
.vscode/
*.swp
EOF

# First commit
git add .
git commit -m "Initial portfolio: index.html, README, theme, supporting docs"
```

Then on GitHub:

1. Go to https://github.com/new
2. **Repository name:** `priyanka-bodagala-portfolio`
3. Public · do **not** initialize with README/license (already have one)
4. Create

Push from your terminal:

```bash
git remote add origin https://github.com/<your-username>/priyanka-bodagala-portfolio.git
git push -u origin main
```

---

## 2. Enable GitHub Pages

1. On the repo → **Settings** → **Pages** (left sidebar).
2. **Source** → *Deploy from a branch*.
3. **Branch** → `main`, **Folder** → `/ (root)`.
4. Click **Save**.
5. Wait ~1–2 minutes. Your site will be live at:

   `https://<your-username>.github.io/priyanka-bodagala-portfolio/`

---

## 3. (Optional) Custom domain

If you own a domain (e.g., `priyankabodagala.com`):

1. Add a `CNAME` file at the repo root containing exactly:
   ```
   priyankabodagala.com
   ```
2. At your DNS provider, create:
   - An `A` record pointing `priyankabodagala.com` to GitHub's IPs:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - A `CNAME` record pointing `www` to `<your-username>.github.io`
3. In Settings → Pages, set **Custom domain** to `priyankabodagala.com` and check **Enforce HTTPS**.

---

## 4. Adding your resume PDF

1. Save your resume as `resume.pdf` in the `assets/files/` folder.
2. Wire any resume link in `index.html` to `assets/files/resume.pdf`.
3. Commit and push:
   ```bash
   git add assets/files/resume.pdf
   git commit -m "Add resume PDF"
   git push
   ```

---

## 5. Updating content

The portfolio is a living document. Every time you have new evidence:

| When this happens… | Update… |
|---|---|
| New publication / DOI lands | `index.html` (Publications card) + `docs/portfolio-data.md` + `README.md` |
| Featured article / press hit | `index.html` (Featured Articles card) + `docs/portfolio-data.md` |
| Speaking gig confirmed | `index.html` (Speaking card) + `docs/portfolio-data.md` |
| New judging / peer review | `index.html` (Judging card) + `docs/portfolio-data.md` |
| New role / promotion | `index.html` (Experience timeline) + `docs/portfolio-data.md` |
| New certification | `index.html` (Certifications card) + `docs/portfolio-data.md` |
| Private evidence (letters, screenshots) | `docs/evidence-index.md` only — keep private |

After editing, push:

```bash
git add -A
git commit -m "Update: <what you changed>"
git push
```

GitHub Pages redeploys in 30–90 seconds.

---

## 6. Local preview

To preview locally before pushing:

```bash
cd "/Users/priyanka/Desktop/Priyanka's Desktop/Portfolio"
python3 -m http.server 8000
# then open http://localhost:8000
```

---

## 7. Quick design tweaks

The colorful theme lives entirely in `assets/css/style.css` under `:root` CSS variables:

- Change brand colors → edit `--color-blue`, `--color-cyan`, `--color-purple`, etc.
- Change hero gradient → edit `--gradient-hero`
- Change card radius → edit `--radius-card`
- Change typography → edit `--font-heading` / `--font-body` (and the matching `<link>` to Google Fonts in `index.html`)

Each section uses `--accent` per card / per metric (set inline) to keep section colors easy to reorder.

---

## 8. Privacy / safety checklist before going public

- [ ] Confirm `docs/evidence-index.md` is in `.gitignore`
- [ ] Confirm phone number and personal address are **not** in `index.html` or `README.md`
- [ ] Confirm no employer-confidential data is in any project description
- [ ] Confirm every external link resolves (publications, featured articles, certifications)
- [ ] Confirm `Profile-linkedin.pdf` and any other private PDFs are **not** committed (add to `.gitignore` if needed)

---

## 9. Recommended `.gitignore` additions

```gitignore
# Private source PDFs (keep local only)
Profile-linkedin.pdf
*.private.pdf

# Drafts
*.draft.md
*.draft.html
```
