# raufschlaeger.github.io

Personal academic homepage of Robert Aufschläger, built with Jekyll in the style
of [Academic Pages](https://academicpages.github.io). Self-contained: custom
layout in `_layouts/default.html` and styling in `assets/css/style.css` — no
remote theme required.

## Editing

- **Profile / sidebar & navigation:** `_config.yml` (`author:` and `nav:`).
  Add your `email`, `orcid`, and `scholar` values to make those links appear.
- **About page:** `index.md`
- **Publications:** `publications.md`
- **Teaching:** `teaching.md`
- **Layout / styling:** `_layouts/default.html`, `assets/css/style.css`

## Testing locally, before committing

You don't need Ruby/Jekyll installed — the official `jekyll/jekyll` Docker image
builds and serves the site exactly as GitHub Pages will.

**PowerShell:**
```powershell
docker run --rm -p 4000:4000 -v "${PWD}:/srv/jekyll" -w /srv/jekyll jekyll/jekyll:4 bash -lc "gem install webrick --no-document && jekyll serve --host 0.0.0.0 --force_polling"
```

**Git Bash:**
```bash
MSYS_NO_PATHCONV=1 docker run --rm -p 4000:4000 -v "$(pwd)":/srv/jekyll -w /srv/jekyll jekyll/jekyll:4 bash -lc "gem install webrick --no-document && jekyll serve --host 0.0.0.0 --force_polling"
```

Then open **http://localhost:4000**. `--force_polling` is required because Docker's
native file-change notifications don't propagate through the Windows→Linux bind
mount — with it, saving a file in the IDE and refreshing the browser picks up the
change within a couple of seconds, no restart needed. Stop the server with `Ctrl+C`.

A stray `ERROR '/favicon.ico' not found.` line in the log is harmless — it comes
from the browser auto-requesting a legacy `/favicon.ico`, which the actual
`<link rel="icon">` in `_layouts/default.html` already replaces.

If you have Ruby installed natively instead, the equivalent is:
```bash
bundle exec jekyll serve
```

**Before committing:** run `git status` / `git diff` to review what you're about
to stage. `_site/`, `.jekyll-cache/`, and Bundler artifacts are already covered by
`.gitignore`, but double-check any config or content changes don't include
personal data (API keys, tokens, unpublished info) you didn't mean to publish —
this is a public repo.

The site is deployed automatically to GitHub Pages on push to `main`.
