# Deploying the Happy Places site to GitHub Pages

This is your step-by-step guide to putting the site live at **happyplazes.com** using GitHub Pages. Your current Wix site stays online the whole time until the final DNS step, so there is no downtime.

Files in this folder:
- `index.html` — the main marketing page
- `host-resources.html` — the Amazon affiliate resources page
- `assets/` — hero and story images (swap these for real photos anytime)
- `CNAME` — tells GitHub Pages your domain is happyplazes.com (already set)

---

## Step 1 — Create the repository
1. On GitHub, click **New repository**.
2. Name it something like `happy-places-site`.
3. Set it to **Public** (GitHub Pages needs Public on the free plan).
4. Click **Create repository**.

## Step 2 — Upload the site files
Either drag-and-drop or use git.

**Drag-and-drop (simplest):**
1. On the empty repo page, click **uploading an existing file**.
2. Drag in `index.html`, `host-resources.html`, `CNAME`, and the `assets` folder.
3. Click **Commit changes**.

**Or with git (the workflow you already use):**
```
git init
git add .
git commit -m "Initial Happy Places site"
git branch -M main
git remote add origin https://github.com/YOURUSERNAME/happy-places-site.git
git push -u origin main
```

## Step 3 — Turn on GitHub Pages
1. In the repo, go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Set branch to **main** and folder to **/ (root)**. Click **Save**.
4. Wait 1–2 minutes. GitHub gives you a temporary address like
   `https://YOURUSERNAME.github.io/happy-places-site/`.
5. Open it and confirm the whole site looks right. **Test everything here before touching your domain.**

## Step 4 — Add your custom domain in GitHub
1. Still in **Settings → Pages**, find **Custom domain**.
2. Type `happyplazes.com` and click **Save**.
   (The included CNAME file already sets this, but confirming it here triggers verification.)
3. Leave **Enforce HTTPS** unchecked for now — you will enable it after DNS is set.

> Important: always add the domain in GitHub **before** changing DNS. Doing DNS first can briefly let someone else claim the domain on Pages.

## Step 5 — Point your DNS to GitHub
This happens wherever your domain's DNS is managed (Wix, or a registrar like GoDaddy/Namecheap — check where happyplazes.com is controlled).

Create these records:

| Type  | Name / Host | Value                | 
|-------|-------------|----------------------|
| A     | @           | 185.199.108.153      |
| A     | @           | 185.199.109.153      |
| A     | @           | 185.199.110.153      |
| A     | @           | 185.199.111.153      |
| CNAME | www         | YOURUSERNAME.github.io |

- The four **A records** point the bare domain (happyplazes.com) at GitHub.
- The **CNAME** points www.happyplazes.com to your GitHub Pages site.
- If Wix currently has old A records or a different setup for the domain, replace them with the above. Remove any conflicting A records pointing at Wix.

## Step 6 — Enable HTTPS
1. Wait for DNS to propagate — usually 15–60 minutes, occasionally longer.
2. Return to **Settings → Pages** and check **Enforce HTTPS**.
   (If it is greyed out, DNS has not finished propagating yet. Wait and check back.)
3. Your site is now live at https://happyplazes.com with a secure padlock.

---

## After you go live
- **Cancel Wix** only after the new site is confirmed live and the domain resolves correctly. If Wix is also your domain *registrar* (not just host), do NOT cancel the domain registration — keep the domain, just repoint DNS.
- **Swap images:** replace `assets/hero.jpg` and `assets/story.jpg` with real photos (same filenames), commit, done.
- **Formspree:** the evaluation form is already wired to your Formspree endpoint. After the site is live, submit the form once yourself to trigger Formspree's one-time confirmation email, then click the link in that email to activate it. After that, all submissions flow to your inbox automatically.
- **Update content:** edit the HTML files, commit, and GitHub Pages redeploys automatically within a minute.

## Updating later
Any change is just: edit file → commit → it's live in about a minute. No rebuild step, no deploy button.
