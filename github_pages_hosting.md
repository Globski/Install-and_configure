# Hosting Static Pages with GitHub Pages

## Description

This guide explains how to host a **static website** (HTML, CSS, JavaScript) using **GitHub Pages**, a free hosting service provided by GitHub.  
Once completed, your site will be accessible from:

```

https\://<your-username>.github.io/<repo-name>/

```

---

## Requirements

- A GitHub account (free).
- A repository with your website files (`index.html`, `style.css`, etc.).
- Git installed on your computer (or use GitHub Desktop).
- Your site must be **static** (not Flask/Django backend).

---

## Table of Contents

1. [Create a GitHub Repository](#1-create-a-github-repository)
2. [Prepare Your Project Files](#2-prepare-your-project-files)
3. [Push Your Code to GitHub](#3-push-your-code-to-github)
4. [Enable GitHub Pages](#4-enable-github-pages)
5. [Access Your Live Website](#5-access-your-live-website)
6. [Common Issues](#6-common-issues)
7. [Tips and Best Practices](#7-tips-and-best-practices)

---

## 1. Create a GitHub Repository

1. Go to [github.com](https://github.com)
2. Click **New Repository**
3. Give it a name, e.g. `my-portfolio`
4. **Make it Public**
5. Optionally check “Add a README”
6. Click **Create Repository**

---

## 2. Prepare Your Project Files

Make sure you have:

- `index.html` (entry point)
- Any other CSS/JS/image files
- Optional: `README.md` and `LICENSE`

📁 Example structure:

```

my-portfolio/
├── index.html
├── style.css
└── script.js

````

Make sure your `index.html` file is in the **root** folder — GitHub Pages looks for it.

---

## 3. Push Your Code to GitHub

### Option A: Using Git CLI

```bash
# Initialize Git
git init

# Link to GitHub
git remote add origin https://github.com/<your-username>/<repo-name>.git

# Track and commit files
git add .
git commit -m "Initial website upload"

# Push to the main branch
git branch -M main
git push -u origin main
````

> 📝 Replace `<your-username>` and `<repo-name>` with your actual GitHub info.

### Option B: Using GitHub Desktop

1. Open GitHub Desktop
2. Click **File → Add Local Repository**
3. Choose your project folder
4. Click **Publish Repository**
5. Make sure it’s public
6. Push changes

---

## 4. Enable GitHub Pages

1. Go to your my-portfolio repo on GitHub
2. Click on **Settings** tab at the top
3. Scroll to **Pages** (on the left or bottom section)
4. Under **"Source"**, select:

   * **Branch:** `main`
   * **Folder:** `/root`
5. Click **Save**

🔁 GitHub will build your site. This usually takes **1–2 minutes**.

---

## 5. Access Your Live Website

After saving, GitHub will show your live link:

```
https://<your-username>.github.io/<repo-name>/
```

---

## 6. Common Issues

| Problem               | Solution                                         |
| --------------------- | ------------------------------------------------ |
| Page not showing?     | Wait 2–5 minutes or clear browser cache          |
| 404 Error?            | Ensure `index.html` is in the root of the repo   |
| Broken CSS or JS?     | Check your file paths — GitHub is case-sensitive |
| You renamed the repo? | You’ll get a new URL — update your bookmarks     |

---

## 7. Tips and Best Practices

* ✅ Use lowercase file and folder names.
* ✅ Keep file paths relative (`./images/pic.png` not `C:\Users\...`)
* ✅ Update your site by:

  ```bash
  git add .
  git commit -m "Update"
  git push
  ```
* ✅ Use [GitHub Actions](https://docs.github.com/en/actions) for auto-deployment (optional advanced).
* ❌ GitHub Pages does **not support Flask, Django, PHP**, or any back-end logic.

---

## ✅ Final Checklist

* [x] `index.html` exists at root
* [x] Code is committed and pushed
* [x] Pages enabled under “Settings”
* [x] Site loads at `https://yourusername.github.io/reponame`

---

### 🙌 Done!

You’ve now deployed a live website using GitHub Pages — 100% free.
Feel free to update and push changes any time!

**Happy Hosting!** 🌍🚀

