# kaniamaciej.github.io

Personal academic website for Maciej Kania, built with the
[portfolYOU](https://github.com/yousinix/portfolYOU) Jekyll theme and hosted on GitHub Pages.

The theme is used as a **remote theme** (see `_config.yml`), so this repo only contains
*content* — the theme engine lives in the portfolYOU repo and is pulled in automatically
when GitHub Pages builds the site.

## How it's organized

| Path | What it controls |
|------|------------------|
| `_config.yml` | Site title, your bio, and social links (email, GitHub, Bluesky). |
| `images/profile.jpg` | Your profile photo (round image on the home page). **Add this file.** |
| `pages/index.md` | Home / landing page (photo + bio + social icons). |
| `pages/about.md` | About page: bio, education + experience timeline, scholarships & funding. |
| `pages/research.md` | Scientific output: papers, preprints, posters, talks, workshops. |
| `pages/community.md` | Community & outreach activities. |
| `pages/projects.html` | Project cards grid. |
| `_data/timeline.yml` | Education & research experience entries. |
| `_data/scientific-output.yml` | All publications, posters, talks, workshops. |
| `_data/community.yml` | Community activity entries. |
| `_data/funding.yml` | Scholarships, fellowships, grants. |
| `_projects/*.md` | One file per project card. |

## To edit content

Most updates are just editing a `_data/*.yml` file — no HTML needed. Each file has
comments and a template entry showing the format. Commit the change and GitHub Pages
rebuilds the site in a minute or two.

## Things to fill in / fix

- Add your photo as `images/profile.jpg`.
- In `_config.yml`: confirm your Bluesky handle, add LinkedIn / Google Scholar / ORCID if wanted.
- In `_data/timeline.yml`: add your earlier degree(s).
- In `_data/scientific-output.yml`: add real links (arXiv / DOI / OpenReview) and fill posters/talks/workshops.
- In `_data/funding.yml`: add your awards.

Theme: portfolYOU by Youssef Raafat Nasry, MIT License.
