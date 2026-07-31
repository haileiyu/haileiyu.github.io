# haileiyu.github.io

Personal site — writing, plus photographs. Built with [Hugo](https://gohugo.io),
hosted free on GitHub Pages.

The design is a deliberate, minimal homage to
[stephenshore.net](https://www.stephenshore.net): white background, Helvetica at
one size, `#555` links, no borders or shadows, and images capped by *height* so
portrait and landscape photographs carry equal weight. See the notes at the top
of `assets/css/main.css` before changing anything there.

## Working on it

```sh
brew install hugo        # extended build; needed for WebP
hugo server              # http://localhost:1313, live-reloads on save
hugo server -D           # include drafts
```

## Writing a post

Text only — one file:

```sh
hugo new content writing/some-post.md
```

Remove `draft: true` from the front matter when it's ready to publish.

With pictures — a folder, with the images sitting next to `index.md`:

```
content/writing/some-post/
    index.md
    kitchen.jpg
```

and in `index.md`:

```
{{</* img src="kitchen.jpg" alt="A kitchen" caption="Brooklyn, 2026" */>}}
```

Photograph posts go in `content/photographs/` instead and use the same layout.
The `photographs` index shows one thumbnail per post — set `cover: "file.jpg"`
in the front matter to choose which image, otherwise the first one is used.

## Images: the one rule

**Resize before you commit.** Git history is permanent — an image you commit
today stays in the repository forever, even if you delete the file later, and
GitHub recommends staying under 1 GB per repo.

Cap the long edge at about 2400px before `git add`. A photo straight off a
camera is 5–12 MB; the same photo at 2400px is a few hundred KB. Hugo takes it
from there, generating 800/1200/1800px WebP variants at build time and
publishing only those — the full-size originals stay in git and never ship to
the browser.

If the site ever gets genuinely photo-heavy, the escape hatch is to host images
outside the repo (Cloudflare R2 or Backblaze B2, both with free tiers).

## Deploying

Push to `main`. The workflow in `.github/workflows/deploy.yml` builds and
publishes; watch it under the repo's Actions tab. Nothing else to do.

## Adding a custom domain later

1. Buy the domain.
2. At the registrar, for the apex (`example.com`) add four A records:
   `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`.
   For `www`, add one CNAME to `haileiyu.github.io`.
3. Create `static/CNAME` containing just the bare domain.
4. Repo Settings → Pages → Custom domain, then tick **Enforce HTTPS**
   (free certificate, may take a few minutes to appear).
5. Update `baseURL` in `hugo.toml` so local builds match.
