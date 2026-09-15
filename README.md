# Ishaque Lab website

Source for [ishaquelab.github.io](https://ishaquelab.github.io), the website of the Ishaque Lab (Cancer Bioinformatics, Charité - Universitätsmedizin Berlin and BIH Center of Digital Health).

The site is a small, dependency-free [Jekyll](https://jekyllrb.com) site built and hosted by GitHub Pages. It is deliberately simple: no theme gem, no build step beyond what GitHub Pages runs for you, no JavaScript framework. Almost all content lives in YAML data files, so day-to-day maintenance means editing a few lines of YAML, not HTML.

Other research groups are welcome to fork it as a starting point. The [Reusing this site](#reusing-this-site-for-your-own-group) section explains what to change.

## Features

- **Seven pages**: Home, Research, Software, Publications, People, Join, Contact.
- **Live publication list** pulled from [OpenAlex](https://openalex.org) by ORCID at page load. Five most recent on the home page; full list with a preprint toggle on the Publications page. No API key, no scheduled job, nothing to update when a paper comes out.
- **Curated "selected publications"** with a one-line rationale each, above the live list.
- **People, software, research themes and consortia** rendered from YAML, with icon links (email, GitHub, Google Scholar, ORCID for people; GitHub, docs, DOI, Zenodo, PyPI, conda-forge, Bioconda and a licence tag for software).
- **Footer** with profile icons and a row of institutional logos, all data-driven.
- **Single stylesheet** (`assets/css/main.css`) with the palette defined as CSS variables at the top, so recolouring the whole site is a five-line edit.
- Responsive, keyboard-accessible, respects `prefers-reduced-motion`, and uses one web font (IBM Plex Sans via Google Fonts; swap for a system stack to remove the external request).

## Repository layout

```
.
├── _config.yml                 site-wide settings and identifiers (title, ORCID, Scholar URL, email)
├── _layouts/default.html       the single page template (head, header, main, footer)
├── _includes/
│   ├── header.html             logo and navigation, built from _data/nav.yml
│   ├── footer.html             address, profile icons, partner logos
│   ├── person.html             one entry on the People page
│   └── tool.html               one entry on the Software page
├── _data/
│   ├── nav.yml                 navigation tabs (title + url)
│   ├── people.yml              lab members, grouped
│   ├── software.yml            tools, grouped
│   ├── projects.yml            research themes (home page grid + Research page sections)
│   ├── consortia.yml           consortia and major projects (Research page)
│   ├── selected_publications.yml
│   └── partners.yml            institutional logos in the footer
├── index.md                    Home
├── research.md                 Research (themes, then consortia)
├── software.md                 Software
├── publications.md             Publications (selected + live OpenAlex list)
├── people.md                   People
├── join.md                     Join (internships, positions)
├── contact.md                  Contact and finding us (address, directions, OpenStreetMap embed)
├── assets/
│   ├── css/main.css            all styling
│   ├── js/publications.js      OpenAlex fetch and rendering
│   └── img/                    logo, favicon, icons, partner logos, people/ photos
└── README.md
```

Pages are Markdown files with YAML front matter (`layout`, `title`, optional `description` for the meta tag). They contain a mix of Markdown and HTML; Liquid loops pull in the data files. Jekyll's `permalink: pretty` setting turns `people.md` into `/people/`.

## Editing content

### Text on a page

Edit the corresponding `.md` file in the repository root. Markdown works anywhere outside an HTML block; inside a `<div>` you need `markdown="1"` on the opening tag for kramdown to process it (see `contact.md`).

### People (`_data/people.yml`)

```yaml
- group: Doctoral researchers          # section heading; groups render in file order
  members:
    - name: Jane Doe
      title: Spatial transcriptomics QC  # optional, one line
      email: jane.doe@example.org        # optional
      github: janedoe                    # optional, username only
      scholar: XXXXXXXXXXXX              # optional, the `user=` value from a Scholar URL
      orcid: 0000-0000-0000-0000         # optional
      photo: /assets/img/people/jane.jpg # optional, square, ~300 px; a monogram is shown if absent
```

Every key except `name` is optional; the template skips missing ones. Move someone between groups by cutting and pasting the block. Alumni are just another group.

### Software (`_data/software.yml`)

```yaml
- group: Tools we lead
  tools:
    - name: SpatialLeiden
      summary: One or two sentences. A citation at the end is conventional.
      repo: https://github.com/org/repo         # GitHub icon
      docs: https://spatialleiden.readthedocs.io # Read the Docs icon
      doi: 10.1186/s13059-025-03489-7            # bare DOI, no https://doi.org/ prefix
      zenodo: https://doi.org/10.5281/zenodo.NNN # optional
      pypi: spatialleiden                        # package name; links to pypi.org
      conda: spatialleiden                       # package name; links to conda-forge
      bioconda: spatialleiden                    # package name; links to Bioconda
      license: GPL-3.0                           # short SPDX identifier, shown as a tag
```

`summary` may contain inline HTML if you need a link in the text; wrap the value in single quotes so the double quotes inside need no escaping.

### Research themes (`_data/projects.yml`)

Each theme has an `id` (used as the anchor on `/research/#id`), a `name`, a `short` one-liner for the home-page grid and a longer `summary` for the Research page. Five themes fit the home grid well; the grid reflows for any number.

### Consortia and major projects (`_data/consortia.yml`)

Each entry has `id`, `name`, `url`, `about` (what the consortium is; attribute claims you did not make), `role` (what your group does in it), an optional `roles_line` for named personal positions, an optional `logo` path, and a `related` list of `{text, url}` links to tools or publications. Multi-line text uses the YAML `>` folded-scalar syntax so paragraphs can be wrapped in the source.

### Selected publications (`_data/selected_publications.yml`)

`citation`, `title`, `doi` (bare DOI) and `why` (one sentence on what the paper contributes). Kept short on purpose: this is the list you want a visitor to read, not the full record.

### Footer logos (`_data/partners.yml`)

`name`, `url`, `img` and a per-logo `height` in pixels, because stacked marks need more height than wide wordmarks to read at the same visual weight. Logos must be white (or a light grey) on a transparent background to sit on the navy footer.

### Navigation (`_data/nav.yml`)

Ordered list of `title` and `url`. Adding a page means adding the `.md` file and one entry here.

### Site identifiers (`_config.yml`)

`orcid`, `scholar`, `github_org`, `email` and `openalex_mailto` are read by the templates and the publications script. Change them once here.

## YAML pitfalls

A syntax error in any `_data/*.yml` file fails the whole build. The usual causes:

- A value containing a colon followed by a space (`title: SpatialLeiden: spatially aware...`). Wrap the value in quotes.
- A value containing ` #` (space-hash), which starts a comment. Quote it.
- A value starting with `[`, `{`, `*`, `&`, `!`, `%`, `@` or a backtick. Quote it.
- Inconsistent indentation. Use two spaces; never tabs.

When a build fails, open the Actions tab, click the failed run and expand the **Build with Jekyll** step. The error names the file and line.

## Publications feed

`assets/js/publications.js` queries `https://api.openalex.org/works?filter=author.orcid:<ORCID>&sort=publication_date:desc`. It runs in the visitor's browser; the site itself never contacts OpenAlex. Any element with a `data-pubs` attribute is filled:

```html
<div data-pubs data-orcid="{{ site.orcid }}" data-limit="5" data-mailto="{{ site.openalex_mailto }}" data-scholar="{{ site.scholar }}"></div>
```

`data-limit` caps the list (200 maximum per request), `data-controls="true"` adds the "include preprints" checkbox, `data-scholar` is the fallback link shown if the request fails. `data-mailto` puts requests in OpenAlex's polite pool, which is faster.

Known limits: OpenAlex lags Google Scholar by days to weeks, occasionally lists a preprint and its journal version separately, and provides no citation counts. If you would rather have a static, reviewable list, replace the script with a GitHub Action that writes `_data/publications.json` on a schedule.

Google Scholar is linked but never queried: it has no API and blocks automated access.

## Styling

All styling is in `assets/css/main.css`. The palette is declared once as CSS custom properties:

```css
:root {
  --navy:  #0B335D;   /* headings, buttons, footer */
  --mid:   #2A5A82;   /* links */
  --light: #4F86AB;   /* accents, active nav */
  --pale:  #6BAACB;   /* light accents */
  --wash:  #EEF3F8;   /* panel backgrounds */
  --rule:  #D5E1EC;   /* hairlines */
  --ink:   #1B2733;   /* body text */
  --ink-2: #4A5966;   /* secondary text */
}
```

These four blues were sampled from the lab logo. To restyle for another group, sample four tones from your own logo and replace them; everything else follows. Icons (`assets/img/*-grey.svg`) are a neutral `#767676`, chosen because it meets WCAG 4.5:1 contrast on both white and black; they need no change when the palette changes.

Icon SVGs come from [Simple Icons](https://simpleicons.org) (CC0) and [Feather](https://feathericons.com) (MIT), recoloured by editing the `fill` attribute.

## Reusing this site for your own group

1. Fork or download the repository into a new repo named `<yourorg>.github.io` (user or organisation site) or any name (project site; then set `baseurl` in `_config.yml` to `/<reponame>`).
2. Edit `_config.yml`: `title`, `tagline`, `description`, `url`, `orcid`, `scholar`, `github_org`, `email`, `openalex_mailto`.
3. Replace the logo files in `assets/img/` and the path in `_includes/header.html`. Regenerate `favicon.png` and `apple-touch-icon.png` from your own mark (a square crop of the logo symbol without the wordmark, exported at 512 and 180 px).
4. Replace the palette in `assets/css/main.css`.
5. Rewrite the `.md` pages. `contact.md` also contains an OpenStreetMap embed with hard-coded coordinates.
6. Replace the contents of every file in `_data/`. Delete `consortia.yml` entries and the corresponding section in `research.md` if you have none.
7. Replace the partner logos in `assets/img/` and `_data/partners.yml`. Check each institution's logo-use guidelines; most permit use by their own members.
8. In the repository settings, under Pages, choose "Deploy from a branch", branch `main`, folder `/ (root)`. The site builds on every push.

Things this site does not do, in case you need them: a blog or news feed, per-person pages, a bibliography from BibTeX, multiple languages. All are standard Jekyll additions.

## Local preview

Optional; GitHub Pages builds on push, so most edits can be made in the web editor and checked on the live site after a minute or two.

```sh
gem install bundler
bundle init
bundle add github-pages --group jekyll_plugins
bundle exec jekyll serve      # http://localhost:4000
```

## Licence

Code (templates, stylesheet, JavaScript, this README) is released under the MIT Licence; see `LICENSE`. The text, photographs and the Ishaque Lab logo are not covered and may not be reused. Institutional and consortia logos belong to their owners.
