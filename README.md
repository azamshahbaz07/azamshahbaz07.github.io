# ePortfolio — Jekyll site for GitHub Pages

## Publish (about 5 minutes)
1. On GitHub, create a **public** repo named `azamshahbaz07.github.io`.
2. Upload every file in this folder to the repo root (drag and drop works) and commit.
3. Repo → **Settings → Pages** → Source: *Deploy from a branch* → `main` / `(root)` → Save.
4. Wait about a minute, then open https://azamshahbaz07.github.io

Using a different repo name? Set `baseurl: "/repo-name"` in `_config.yml`.

## Where things live
| Change this | Edit this file |
|---|---|
| Name, email, LinkedIn, menu | `_config.yml` |
| Home / About / Experience / Career / Contact text | `index.md`, `about.md`, `experience.md`, `career.md`, `contact.md` |
| Roadmap stages | `_data/roadmap.yml` |
| A project | `_projects/<name>.md` (new file = new project card) |
| Resume | replace `assets/resume.pdf` |
| Images | `assets/img/` |
| Colors / fonts | `assets/css/style.css` (tokens at the top) |

## Adding a project
Copy any file in `_projects/`, change the front matter (`title`, `category`: discovery / software / hardware, `summary`, `stack`, `image`), and write the body. It shows up on the Projects page automatically. Set `featured: true` to also show it on the home page.

## Preview locally (optional)
`bundle install && bundle exec jekyll serve` → http://localhost:4000
