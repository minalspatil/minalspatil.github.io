# minalspatil.github.io

Personal website of Minal Suresh Patil, built with [Jekyll](https://jekyllrb.com/) and the [al-folio](https://github.com/alshedivat/al-folio) theme, hosted on GitHub Pages.

## Edit content

- Homepage: `_pages/about.md`
- Publications: `_bibliography/papers.bib` (add `selected={true}` to show a paper on the homepage)
- CV: `_data/cv.yml` and `assets/pdf/MSP.pdf`
- Site settings: `_config.yml`

## Run locally

```bash
bundle install
bundle exec jekyll serve
```

Pushes to `main` build and deploy via `.github/workflows/deploy.yml`.
