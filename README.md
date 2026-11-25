# alletogether.com - GitHub Pages site

One-page static site for AlleTogether. It directs visitors to the AlleFashion store on Amazon:

https://www.amazon.com/s?rh=n%3A7141123011%2Cp_4%3AAlleFashion&ref=bl_sl_s_ap_web_7141123011

No server, no build step, hosting is $0 on GitHub Pages.

## Files in this folder
- `index.html` - the page, Amazon link is already plugged in
- `CNAME` - contains `alletogether.com`, tells GitHub Pages the custom domain
- `.nojekyll` - tells GitHub Pages to serve the files as-is

## Before you deploy: re-register the domain
Checked Nov 14, 2026: alletogether.com returned NXDOMAIN and a registry 404, so it appears dropped / unregistered, not just offline.
Re-register it first (about $11.17/yr at Cloudflare Registrar, about $11.81/yr at Porkbun). You will need access to that registrar account to add the DNS records below.

## Deploy to GitHub Pages - 5 minutes

1. Create a new **public** repo on GitHub, named `alletogether.github.io`
   - this is your user site repo, so its default address will be https://alletogether.github.io which matches the brand

2. Push this folder to that repo from your Mac:
```bash
cd alletogether-site
git init
git add index.html CNAME .nojekyll README.md
git commit -m "AlleTogether landing page"
git branch -M main
git remote add origin https://github.com/alletogether/alletogether.github.io.git
git push -u origin main
```

3. In the repo on github.com: **Settings > Pages**
   - Source: Deploy from a branch
   - Branch: `main` / `(root)`, then Save
   - Custom domain: `alletogether.com` (it should already read this from the CNAME file), then Save
   - After DNS checks pass, tick **Enforce HTTPS**

4. Add DNS at your registrar for alletogether.com:
   - Apex ( @ ) A records - add all four:
     - 185.199.108.153
     - 185.199.109.153
     - 185.199.110.153
     - 185.199.111.153
   - Apex AAAA records (optional, for IPv6):
     - 2606:50c0:8000::153
     - 2606:50c0:8001::153
     - 2606:50c0:8002::153
     - 2606:50c0:8003::153
   - `www` CNAME record:
     - Host: `www`
     - Value: `alletogether.github.io`

5. Wait for DNS to propagate (usually 15 min to a few hours, up to 24h). GitHub will provision a free Lets Encrypt HTTPS certificate automatically once DNS is correct.
   Then https://alletogether.com and https://www.alletogether.com should both show the page, and the button goes to Amazon.

## Changing the Amazon link later
Edit the one `<a class="btn" href="...">` link in `index.html`, commit, and push. GitHub Pages redeploys in about a minute.

## Note on GitHub Pages terms
GitHub says Pages is not intended as a free host to run an online business / e-commerce site. This site does not sell or take payments itself, it is a brand landing page linking out to Amazon, which is the low-risk use case. If GitHub ever flags it, the same files deploy unchanged to Cloudflare Pages for $0.
