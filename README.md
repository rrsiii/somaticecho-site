# somaticecho-site

The public, customer-facing site for **SomaticEcho** — landing page, support, and privacy
policy. Static HTML/CSS, hosted free on GitHub Pages at `somaticecho.com`. No backend, no build step.

This repo is intentionally separate from the engine monorepo: it's the only outward-facing
surface, and it ships nothing but flat files.

## Structure

```
index.html            Landing page
support/index.html    Support  → App Store "Support URL"  (somaticecho.com/support)
privacy/index.html    Privacy Policy → App Store "Privacy Policy URL" (somaticecho.com/privacy)
404.html              Fallback page
assets/styles.css     Shared styles (palette pulled from the app)
assets/echo-mark.svg  The Echo orb mark (favicon + hero)
CNAME                 Custom domain for GitHub Pages (somaticecho.com)
.nojekyll             Serve files as-is (skip Jekyll processing)
robots.txt, sitemap.xml
```

## Apple App Store URLs

- **Support URL:** `https://somaticecho.com/support`
- **Privacy Policy URL:** `https://somaticecho.com/privacy`
- **Marketing URL** (optional): `https://somaticecho.com`

## Before publishing — review the privacy policy

The privacy policy is a drafted starting point, not legal advice. Search the source for
`REVIEW:` comments and confirm each one (effective date, legal entity name, the exact list
of data processors, the audio-handling claims, the minimum age). Get a lawyer's eyes on it
if you can before you rely on it.

## Deploy (one time)

1. Create a new **public** GitHub repo named `somaticecho-site` (empty, no README).
2. From this folder:
   ```sh
   git init
   git add -A
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/somaticecho-site.git
   git push -u origin main
   ```
3. On GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   branch `main`, folder `/ (root)`. Save.
4. Still on **Settings → Pages**, under *Custom domain* it should already show
   `somaticecho.com` (from the `CNAME` file). Tick **Enforce HTTPS** once it's available.

## DNS — point the domains

At your domain registrar (where you bought `somaticecho.com` / `somaticecho.ai`):

**`somaticecho.com` (apex) → GitHub Pages.** Add four `A` records:
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```
(Optionally also `AAAA` records to `2606:50c0:8000::153`, `…8001::153`, `…8002::153`, `…8003::153`.)
If you also want `www.somaticecho.com`, add a `CNAME` record `www → <your-username>.github.io`.

**`somaticecho.ai` → redirect to `somaticecho.com`.** Simplest is a registrar-level
"domain forwarding / redirect" rule (most registrars offer this) pointing `somaticecho.ai`
→ `https://somaticecho.com`. No GitHub setup needed for the `.ai`.

DNS + HTTPS provisioning can take anywhere from a few minutes to a day.

## Email — make support@ work

`support@somaticecho.com` is referenced across the site but won't receive mail until you set
up email forwarding/hosting on the domain. Most registrars offer free email forwarding
(`support@somaticecho.com` → your inbox); set that up before submitting to Apple, since
reviewers may test the address.

## Editing

Plain HTML — open a file, edit, commit, push. GitHub Pages redeploys automatically.
Keep copy on-brand: read `docs/brand-spine.md` in the engine repo first. **No medical claims, ever.**
