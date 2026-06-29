# PlateHub

Three free meal planning tools on one domain.

- **SteadyPlate** — weekly meal planner with calorie & macro tracking
- **LazyPlate** — AI-powered recipe finder from whatever's in your fridge
- **PetPlate** — pet food safety checker with portion guidance

---

## Setup: GitHub Pages (free hosting)

### Step 1 — Create the repository

1. Go to [github.com](https://github.com) and sign in (or create a free account)
2. Click **New repository**
3. Name it `platehub` (or anything you like)
4. Set it to **Public**
5. Click **Create repository**

### Step 2 — Upload the files

**Option A — GitHub web interface (easiest):**
1. In your new repo, click **Add file → Upload files**
2. Drag and drop the entire `platehub` folder contents
3. Click **Commit changes**

**Option B — Git CLI:**
```bash
cd platehub
git init
git add .
git commit -m "Initial PlateHub launch"
git branch -M main
git remote add origin https://github.com/YOURUSERNAME/platehub.git
git push -u origin main
```

### Step 3 — Enable GitHub Pages

1. In your repo, go to **Settings → Pages**
2. Under **Source**, select **Deploy from a branch**
3. Select **main** branch, **/ (root)** folder
4. Click **Save**

Your site will be live at `https://YOURUSERNAME.github.io/platehub/` within a few minutes.

---

## Add your API key

The AI tools (LazyPlate, PetPlate, SteadyPlate) call the Anthropic API. You need to add your API key.

**In each tool file, find this line:**
```javascript
headers: { 'Content-Type': 'application/json' },
```

**Replace with:**
```javascript
headers: {
  'Content-Type': 'application/json',
  'x-api-key': 'YOUR_API_KEY_HERE',
  'anthropic-version': '2023-06-01',
  'anthropic-dangerous-direct-browser-access': 'true'
},
```

Files to update:
- `lazyplate/index.html`
- `petplate/index.html`
- `steadyplate/index.html`

Get your API key at [console.anthropic.com](https://console.anthropic.com).

> **Note:** For a production site, use a backend proxy so your API key isn't exposed in the browser. For launch/MVP, direct browser access is fine.

---

## Connect a custom domain (platehub.com)

1. Buy `platehub.com` at [Namecheap](https://namecheap.com), [Porkbun](https://porkbun.com), or [Cloudflare](https://cloudflare.com)
2. In your registrar's DNS settings, add:
   ```
   Type: A    Name: @    Value: 185.199.108.153
   Type: A    Name: @    Value: 185.199.109.153
   Type: A    Name: @    Value: 185.199.110.153
   Type: A    Name: @    Value: 185.199.111.153
   Type: CNAME Name: www  Value: YOURUSERNAME.github.io
   ```
3. In GitHub repo **Settings → Pages → Custom domain**, enter `platehub.com`
4. Check **Enforce HTTPS** (appears after DNS propagates, ~10 minutes)

---

## Add Google AdSense

1. Apply at [adsense.google.com](https://adsense.google.com) — you need the custom domain live first
2. Once approved, add the AdSense script to the `<head>` of each HTML file:
   ```html
   <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-XXXXXXXXXXXXXXXX" crossorigin="anonymous"></script>
   ```
3. Place ad units in the layout where you want them to appear

---

## File structure

```
platehub/
├── index.html          ← Homepage
├── privacy.html        ← Privacy policy
├── styles/
│   └── main.css        ← Shared design system
├── lazyplate/
│   └── index.html      ← LazyPlate tool
├── steadyplate/
│   └── index.html      ← SteadyPlate tool
└── petplate/
    └── index.html      ← PetPlate tool
```

---

## SEO checklist

- [ ] Submit sitemap to Google Search Console after going live
- [ ] Add Google Analytics (`gtag`) to all pages
- [ ] Add Open Graph meta tags for social sharing
- [ ] Each tool page has its own title + meta description (already set)
- [ ] Update footer year if needed

---

## License

All rights reserved. PlateHub is a private project.
