# Deploy this site to GitHub Pages — step by step

This folder is a complete, self-contained static site. You will host it as your
**personal GitHub Pages site**, so the live URL becomes:

    https://Tianhao1314.github.io

(One personal Pages site per GitHub account; takes ~5 minutes the first time.)

---

## Step 0 — Prereqs

If you don't already have a GitHub account, create one at
<https://github.com/signup>. Pick a clean username — it shows up in your URL,
your CV, and your application emails. Examples that work well: `tianhaowu`,
`Tianhao1314`, `tianhaowu-fau`.

You'll also need `git` installed. On macOS, `git --version` should already work;
if it asks to install developer tools, just say yes.

---

## Step 1 — Swap the placeholders

Before you push anything, open `index.html` and find/replace **`Tianhao1314`**
with your actual GitHub username. There are three occurrences. Also one
`YOUR-SCHOLAR-ID` placeholder for the Google Scholar link — if you don't have
a Scholar profile yet, just delete that whole `<a>` link card.

Quick one-liner from terminal (replace `tianhaowu` with your real username):

```bash
cd "/Users/wutianhao/Library/CloudStorage/OneDrive-个人/Obsidian/MainVault/50-Areas/Personal/PublicPresence/site"
sed -i '' 's/Tianhao1314/tianhaowu/g' index.html
```

Open `index.html` in a browser (double-click) to sanity-check the layout
before pushing.

---

## Step 2 — Push to GitHub

**Path A — with the GitHub CLI (recommended, ~30 seconds).**

If you have `gh` installed (`gh --version` to check; install via `brew install gh`
if not):

```bash
cd /path/to/this/site/folder
gh auth login                          # one-time, follow prompts
gh repo create Tianhao1314.github.io --public --source=. --remote=origin --push
```

That's it. Your site is live at `https://Tianhao1314.github.io` within ~1 minute.

**Path B — without gh CLI, via the web.**

1. Go to <https://github.com/new>
2. Repository name: **`Tianhao1314.github.io`** (exact format; this magic name
   tells GitHub to publish it as your personal Pages site)
3. Public, no README/`.gitignore`/license — leave empty.
4. Click "Create repository".
5. In your terminal:

```bash
cd /path/to/this/site/folder
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin git@github.com:Tianhao1314/Tianhao1314.github.io.git
git push -u origin main
```

(If `git@github.com:…` fails with permission denied, use the HTTPS form:
`git remote add origin https://github.com/Tianhao1314/Tianhao1314.github.io.git`
and push; GitHub will prompt for a personal access token instead of a
password.)

---

## Step 3 — Enable Pages (only needed if it doesn't auto-publish)

Modern GitHub auto-publishes the `main` branch for `username.github.io` repos.
If after ~2 minutes `https://Tianhao1314.github.io` still shows a 404:

1. Go to the repo on GitHub
2. **Settings → Pages**
3. Source: **Deploy from a branch** → Branch: **main** → Folder: **/ (root)**
4. Save. Refresh after 1–2 minutes.

---

## Step 4 — Verify

Open `https://Tianhao1314.github.io` in a browser. You should see:

- Your photo and name at the top
- The "About" paragraph
- The blog post on tele-impedance, with the SVG architecture diagram
- A "Links" row with GitHub / Scholar / Email
- All external links open correctly

> Note: the CV PDF is intentionally **not** hosted on this public site
> (your decision, 2026-05-16). If you later want to expose it, drop the
> latest PDF into this folder as `cv.pdf` and re-add a `<a href="cv.pdf">`
> link card to `index.html` (one in the header contact line + one in the
> Links section).

Once it's up, **add the URL to**:
- Your CV (replace the email-only contact line, or add it next to email)
- Your master's thesis cover page
- The signature of any application email
- The Sierotowicz / Castellini email signature

---

## Step 5 — Future updates

The whole site is plain HTML. To change anything:

```bash
cd /path/to/this/site/folder
# edit index.html / blog_post.md / replace photo.png / etc.
git add .
git commit -m "Update site"
git push
```

Changes go live within ~30 seconds.

---

## What's in this folder

| File | What it is |
|---|---|
| `index.html` | The site. Single file. Everything inline (CSS, SVG). |
| `architecture.svg` | Standalone copy of the architecture diagram (handy for slides / papers). |
| `photo.png` | Your portrait, used in the header. |
| `blog_post.md` | Markdown version of the same blog post (handy for re-publishing on Medium, arXiv-style blogs, etc.). |
| `DEPLOY.md` | This file. Will be on the GitHub repo but not on the live site (won't render unless someone navigates to it). |

If you ever decide you don't like the single-file approach (e.g. you want
multiple blog posts, a proper static site generator), you can migrate later
to Jekyll, Hugo or Astro — but for the first 6–12 months and 1–3 posts, plain
HTML is faster to update and less likely to break.
