# XMPro Platform Documentation

Product documentation for the XMPro Platform, published to GitHub Pages with versioned deployment.

**Live site**: [docs.xmpro.com](https://docs.xmpro.com)
**Repository**: [XMPro-Auto/xm-platform-docs](https://github.com/XMPro-Auto/xm-platform-docs)

## Architecture

The site is built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) and deployed to GitHub Pages using [mike](https://github.com/jimporter/mike) for multi-version support. GitHub Actions handles CI/CD: pushes to version branches trigger `mike deploy`, and pull requests run Markdown linting (markdownlint) and link checking (lychee).

## Versions

Each platform version maps to a branch. The `main` branch always represents the current release and is set as the default version on the live site.

| Branch | Version | Status | Deployed |
|--------|---------|--------|----------|
| `main` | 4.6 | Current release | Yes |
| `v4.5` | 4.5 | Supported | Yes |
| `v4.4` | 4.4 | Legacy | Yes |
| `v5.0` | 5.0 | Pre-release | No (commented out in workflow) |

To activate v5.0 deployment, uncomment the `v5.0` lines in `.github/workflows/deploy-docs.yml` (both the branch trigger and the case statement).

## Theme and styling

The site's visual design is aligned with the existing DocFX documentation at documentation.xmpro.com. All customisation lives in two places:

- **`docs/stylesheets/extra.css`**: Brand colours (`#121212` header, `#00B0F0` accent), system font stack (no Google Fonts), heading sizes matching DocFX, and dark/light colour scheme definitions.
- **`overrides/main.html`**: Replaces the default Material tabs block with two fixed external links (XMPro Workflow docs and Support portal).

The dark/light toggle is configured in `mkdocs.yml` (two palette entries). Logo swapping between schemes is handled entirely in CSS: `logo-dark.png` (white text) displays on the dark scheme, `logo-light.png` (dark text) on the light scheme.

## Directory structure

```
xm-platform-docs/
├── .github/workflows/
│   ├── deploy-docs.yml        # mike deploy on push to version branches
│   └── validate-docs.yml      # markdownlint + lychee on PRs
├── docs/
│   ├── stylesheets/extra.css  # all custom CSS
│   ├── images/                # logos, favicon
│   └── ...                    # content sections (concepts/, how-tos/, etc.)
├── overrides/
│   └── main.html              # header nav override (external links)
├── mkdocs.yml                 # site config, nav, theme, plugins
├── CONTRIBUTING.md            # editing conventions and PR workflow
└── README.md
```

## Local preview

```bash
git clone https://github.com/XMPro-Auto/xm-platform-docs.git
cd xm-platform-docs
pip install mkdocs-material mike
mkdocs serve
```

Then open [http://localhost:8000](http://localhost:8000). To preview a specific version branch, check it out first (`git checkout v4.5`).

## Deployment

Deployment is automatic. When you push to a version branch (`main`, `v4.5`, `v4.4`), the `deploy-docs.yml` workflow runs `mike deploy` to publish that version to the `gh-pages` branch. Pushes to `main` also set the default version, so the root URL always serves the current release.

Deployments use a concurrency group with `cancel-in-progress: false`, meaning they queue rather than cancel each other. This prevents corruption of the `gh-pages` branch when multiple pushes land in quick succession.

## Adding a new version

1. Create the version branch (e.g., `v5.0`) from the appropriate base.
2. In `deploy-docs.yml` on `main`, uncomment the branch in the `on.push.branches` list and the corresponding `case` entry.
3. Push to the new branch. The workflow will deploy it as a selectable version on the site.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for branch targeting rules, commit conventions, Markdown standards, and the PR workflow.
