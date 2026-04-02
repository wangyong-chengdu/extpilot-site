# ExtPilot Site

Static site for [extpilot.com](https://extpilot.com) — hosted on GitHub Pages.

## Structure

```
extpilot-site/
├── index.html                      # Brand homepage
├── privacy/
│   ├── shopify-spy/index.html      # Shopify Store Scraper privacy policy
│   └── template.html               # Privacy policy template for new extensions
├── CNAME                           # Custom domain config
└── README.md
```

## Deployment

### 1. Create GitHub Repository

```bash
# Option A: User/org site (repo name must be extpilot.github.io)
gh repo create extpilot/extpilot.github.io --public

# Option B: Project site (any repo name)
gh repo create extpilot/extpilot-site --public
```

### 2. Push Code

```bash
cd extpilot-site
git init
git add .
git commit -m "Initial site: homepage + privacy policies"
git remote add origin git@github.com:extpilot/extpilot-site.git
git push -u origin main
```

### 3. Enable GitHub Pages

1. Go to repo **Settings** > **Pages**
2. Source: **Deploy from a branch**
3. Branch: **main** / root
4. Save

GitHub will detect the `CNAME` file and configure the custom domain automatically.

### 4. Configure Cloudflare DNS

Add these DNS records in your Cloudflare dashboard for `extpilot.com`:

**Option A: Apex domain (extpilot.com)**

| Type | Name | Content |
|------|------|---------|
| A    | @    | 185.199.108.153 |
| A    | @    | 185.199.109.153 |
| A    | @    | 185.199.110.153 |
| A    | @    | 185.199.111.153 |

**Option B: Also add www subdomain**

| Type  | Name | Content       |
|-------|------|---------------|
| CNAME | www  | extpilot.github.io |

**Important:** Set Cloudflare proxy status to **DNS only** (gray cloud) for GitHub Pages to work correctly with HTTPS.

### 5. Verify

After DNS propagation (usually a few minutes):
- https://extpilot.com should show the homepage
- https://extpilot.com/privacy/shopify-spy/ should show the privacy policy
- GitHub Pages will auto-provision an SSL certificate

## Adding a New Extension Privacy Policy

1. Copy `privacy/template.html` to `privacy/[extension-slug]/index.html`
2. Replace all `[PLACEHOLDER]` values marked with comments
3. Add the extension to the homepage `index.html`
4. Commit and push
