# Sky Group Services - Static Site Setup Guide

## What This Is

A static clone of https://skygroupservices.com/ (WordPress) converted for free hosting on GitHub Pages. The site is visually identical — all 3 pages (Home, Our Work, Contact Us), CSS, JS, images, and fonts are preserved.

---

## Step 1: Create a GitHub Repository

1. Go to https://github.com/new
2. Repository name: `skygroupservices.com` (or any name you prefer)
3. Set to **Public** (required for free GitHub Pages on a personal account)
4. Do NOT initialize with README, .gitignore, or license
5. Click **Create repository**

---

## Step 2: Push the Static Site to GitHub

Open a terminal in this project folder and run:

```bash
cd /home/ubuntu/dev/ai/skygroupservices

# Rename branch to main
git branch -m main

# Create first commit
git add -A
git commit -m "Static clone of skygroupservices.com"

# Add your GitHub repo as remote (replace YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/skygroupservices.com.git

# Push
git push -u origin main
```

---

## Step 3: Enable GitHub Pages

1. Go to your repo on GitHub → **Settings** → **Pages** (left sidebar)
2. Under **Source**, select **Deploy from a branch**
3. Branch: **main**, folder: **/ (root)**
4. Click **Save**
5. Wait 1-2 minutes — GitHub will build and deploy
6. Your site will be live at: `https://YOUR_USERNAME.github.io/skygroupservices.com/`

---

## Step 4: Configure Custom Domain on GitHub

1. Still in **Settings** → **Pages**
2. Under **Custom domain**, enter: `skygroupservices.com`
3. Click **Save**
4. Check **Enforce HTTPS** (may take a few minutes to become available)

> The CNAME file is already included in the repo. GitHub uses it to know which custom domain to serve.

---

## Step 5: Update DNS at Your Domain Registrar

Log into wherever you registered `skygroupservices.com` (GoDaddy, Namecheap, Cloudflare, etc.) and update the DNS records:

### Remove Existing Records
- Delete any existing **A records** pointing to your old hosting IP
- Delete any existing **CNAME** record for `www`

### Add GitHub Pages DNS Records

**For the apex domain (`skygroupservices.com`)** — add these 4 A records:

| Type | Name | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

**For the www subdomain** — add this CNAME record:

| Type | Name | Value |
|------|------|-------|
| CNAME | www | YOUR_USERNAME.github.io |

> Replace `YOUR_USERNAME` with your actual GitHub username.

---

## Step 6: Verify DNS & HTTPS

1. DNS propagation takes **5 minutes to 48 hours** (usually under 1 hour)
2. Check propagation: https://www.whatsmydns.net/#A/skygroupservices.com
3. Once DNS has propagated, go back to **Settings** → **Pages** and check **Enforce HTTPS**
4. GitHub will automatically provision a free SSL certificate via Let's Encrypt

---

## Step 7: Cancel Old Hosting

Once you've confirmed the site works on GitHub Pages:

1. Verify all 3 pages load correctly:
   - https://skygroupservices.com/
   - https://skygroupservices.com/portfolio/
   - https://skygroupservices.com/contact-us/
2. Test on mobile
3. Cancel your WordPress hosting subscription

---

## Cutover Checklist

- [ ] GitHub repo created and code pushed
- [ ] GitHub Pages enabled (Settings → Pages → main branch)
- [ ] Custom domain set in GitHub Pages settings
- [ ] DNS A records updated (4 GitHub IPs)
- [ ] DNS CNAME for www added
- [ ] DNS propagated (check whatsmydns.net)
- [ ] HTTPS enforced in GitHub Pages settings
- [ ] All pages loading correctly
- [ ] Old hosting cancelled

---

## Important Notes

- **No contact form**: The original WordPress contact form won't work on a static site. The contact page shows your email and phone — visitors can reach you directly.
- **No search/comments**: WordPress dynamic features don't work on static sites. Your site didn't visibly use these anyway.
- **Free forever**: GitHub Pages is free for public repositories with no bandwidth limits for normal traffic.
- **To make changes**: Edit the HTML/CSS files directly and push to GitHub. Changes deploy automatically in ~1 minute.

---

## File Structure

```
├── index.html              # Homepage
├── portfolio/index.html    # Our Work page
├── contact-us/index.html   # Contact Us page
├── 404.html                # Custom 404 page
├── CNAME                   # Custom domain config
├── .nojekyll               # Tells GitHub not to use Jekyll
├── robots.txt              # Search engine config
├── wp-content/             # All CSS, JS, images, fonts
│   ├── plugins/            # RevSlider, LayerSlider, etc.
│   ├── themes/bridge/      # Bridge theme assets
│   └── uploads/            # Your images
└── wp-includes/            # jQuery and WordPress JS libraries
```
