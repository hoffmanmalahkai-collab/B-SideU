# B-SideU Services — website

A complete, self-contained website. **No build step, no framework, no Node.** It is plain
HTML, CSS and JavaScript in one file plus an `assets/` folder, so it runs on literally any
host — and it will still open in a browser in ten years.

To preview it right now: double-click `index.html`.

---

## What's in here

| File | What it is |
| --- | --- |
| `index.html` | The entire site — content, styles and scripts in one file |
| `404.html` | Branded "page not found" page |
| `assets/` | Logo, event photo, favicons, social share image |

**The hero photo is embedded inside `index.html`**, so the page always renders with it even on its own. `assets/event.jpg` is the same photo as a normal file, there if you want it for social posts or flyers.

**About the logo.** `logo-mark.svg` and `logo-lockup.svg` are true vector versions of your
mark — they stay razor sharp at any size, from a favicon to a banner, and each is about
7 KB. The site uses these. The matching `.png` files are high-resolution exports for places
that will not take an SVG (email signatures, Instagram, most print shops).

If you still have the original artwork file the logo was drawn in, that beats any rebuild —
send it over and it can be swapped in.
| `robots.txt` | Tells search engines to index the site |
| `sitemap.xml` | Helps Google find the page |
| `site.webmanifest` | Lets phones "Add to Home Screen" with your logo |
| `_headers`, `_redirects` | Caching and routing for Netlify / Cloudflare Pages |
| `.htaccess` | Same, for Apache / cPanel / most shared hosting |
| `.nojekyll` | Stops GitHub Pages from mangling the files |

Files that don't apply to your host are simply ignored. Upload all of them.

---

## Step 1 — Set your domain (2 minutes)

Three files contain a placeholder domain, `bsideuservices.com`. Search and replace it with
your real domain everywhere in `index.html`, `robots.txt` and `sitemap.xml`.

On Mac or Linux, from inside this folder:

```bash
grep -rl 'bsideuservices.com' . | xargs sed -i '' 's|bsideuservices.com|yourdomain.com|g'
```

(On Linux, drop the `''` after `-i`.)

This only affects the social-share preview and search engines. The site works fine
without doing it — it just won't show a nice preview card when someone shares the link.

---

## Step 2 — Make the contact form deliver to your inbox (5 minutes)

**Out of the box the form already works.** With no setup, pressing "Send inquiry" opens the
visitor's email app with every field filled in, addressed to you. That is fine, but some
people abandon it.

To have inquiries land in your inbox without the visitor leaving the page, pick a free form
service and paste its endpoint into one line.

1. Sign up at **[formspree.io](https://formspree.io)** (free tier covers a small business),
   or Basin, Getform or Web3Forms — they all work the same way.
2. Create a form. It gives you a URL like `https://formspree.io/f/abcdwxyz`.
3. Open `index.html`, find this line near the bottom (search for `FORM_ENDPOINT`):

   ```js
   var FORM_ENDPOINT = "";
   ```

4. Paste your URL between the quotes:

   ```js
   var FORM_ENDPOINT = "https://formspree.io/f/abcdwxyz";
   ```

5. Save, re-upload, and send yourself a test.

**On Netlify** you can skip all of that: add `netlify` and `name="contact"` to the `<form>`
tag and Netlify captures submissions itself, no third party needed.

The form already includes a hidden honeypot field that catches most spam bots.

---

## Step 3 — Put it online

Pick whichever of these suits you. All of them work with these exact files.

### Netlify — easiest, free, custom domain included
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop).
2. Drag this whole folder onto the page.
3. It is live in about ten seconds on a `*.netlify.app` address.
4. Site settings → Domain management → add your own domain when you have one.

To update later, drag the folder again.

### Cloudflare Pages — free, fastest network
1. [dash.cloudflare.com](https://dash.cloudflare.com) → Workers & Pages → Create → Pages.
2. Choose "Upload assets" and drop this folder in.
3. Build command: leave **empty**. Output directory: `/`.

### GitHub Pages — free, versioned
1. Push these files to a GitHub repo.
2. Repo → Settings → Pages → Source: "Deploy from a branch" → `main` → `/ (root)`.
3. Live at `https://yourname.github.io/reponame/` in a minute or two.

The `.nojekyll` file is already here, which GitHub Pages needs.

### Vercel
1. [vercel.com/new](https://vercel.com/new) → import the repo, or drag the folder.
2. Framework preset: **Other**. Build command: leave empty. Output directory: `./`.

### Regular web hosting (GoDaddy, Bluehost, HostGator, Namecheap, any cPanel host)
1. Open your host's File Manager, or connect over FTP with FileZilla.
2. Upload everything into `public_html/` (or `www/`), keeping the `assets/` folder intact.
3. Done. `.htaccess` handles caching and the 404 page automatically.

### Your own server (nginx, Apache, Caddy)
Copy the folder into the web root. It is a static site; nothing needs to run.

### No host at all
The site works straight off a USB stick or your own laptop — just open `index.html`.

---

## Editing the site

Everything is in `index.html`, in plain English, in the order it appears on the page.
Open it in any text editor (VS Code, Notepad, TextEdit in plain-text mode) and search for
the words you want to change.

Common edits:

| To change | Search for |
| --- | --- |
| Phone numbers | `518` — appears in the header, contact section, footer and 404 page |
| Email address | `bsideumusicservices` |
| Prices and minimums | `rate-card` |
| Services offered | `id="services"` |
| FAQ questions | `id="faq"` |
| Towns you serve | `marquee-track` |
| The hero photo | replace `assets/event.jpg` with your own, same filename |

**After editing, always test on your phone.** The layout is built mobile-first but a long
new headline can still push things around.

### Adding real reviews

Nothing on the site claims a review you haven't received — deliberately. Once you have two
or three genuine ones with permission to quote, they are worth adding just above the
contact section. Ask and it can be built to match.

---

## Good to know

- **The logo is embedded directly in `index.html`** as vector code, so the header and footer
  logos can never break, even if the page is opened on its own with no `assets/` folder
  beside it. The files in `assets/` are there for everything else you might need them for.
- **Motion**: the logo draws itself in on load, the headline rises into place, a red progress
  bar tracks scroll across the top, the step numbers count up, the process timeline fills as
  you scroll, and the header condenses once you leave the top. All of it switches off
  automatically for visitors who have "reduce motion" turned on.
- **Dark mode** is built in. The site follows whatever the visitor's phone or laptop is set to.
- **Accessibility**: keyboard navigation, screen-reader landmarks, visible focus rings, and
  it respects "reduce motion" settings.
- **Search engines**: the page carries LocalBusiness and FAQ structured data, so Google can
  show your phone number, service area and pricing directly in results. After going live,
  add the site to [Google Search Console](https://search.google.com/search-console) and
  claim your [Google Business Profile](https://business.google.com) — for a local service
  business those two matter more than anything else on this page.
- **Fonts** load from Google Fonts. If that ever fails, the site falls back to clean system
  fonts and still looks right.
- **Speed**: the whole page is roughly 400 KB, most of it the one photo.
