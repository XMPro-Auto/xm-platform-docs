# Contributing to XMPro Platform Documentation

## Repository structure

This repository uses a branch-per-version model. Each XMPro platform version has its own long-lived branch:

| Branch | Platform version | Status |
|--------|-----------------|--------|
| `main` | v4.6 | Current release |
| `v4.5` | v4.5 | Supported |
| `v4.4` | v4.4 | Legacy |
| `v5.0` | v5.0 | Pre-release |

All documentation content lives under the `docs/` directory. The site is built automatically by MkDocs Material and deployed via GitHub Pages whenever changes are pushed to a version branch.

## Making changes

### Which branch should I target?

Target your PR at the branch matching the platform version your change applies to. Most changes will target `main` (the current release). If a fix applies to multiple versions, submit separate PRs or cherry-pick across branches.

### Browser editing (small changes)

1. Navigate to the file you want to edit on the correct branch
2. Click the pencil icon ("Edit this file")
3. Make your changes and click "Propose changes"
4. Ensure the PR targets the correct branch

### Local editing (larger changes)

1. Clone the repo: `git clone https://github.com/XMPro-Auto/xm-platform-docs.git`
2. Check out the target branch: `git checkout main` (or `v4.5`, etc.)
3. Create a feature branch: `git checkout -b docs/your-change-description`
4. Make changes
5. Preview locally: `pip install mkdocs-material mike && mkdocs serve`
6. Commit with prefix: `git commit -m "docs: your change description"`
7. Push and create a PR targeting the version branch

### Requesting changes via issues

Open an issue using the documentation update template. A maintainer will triage it to the correct version branch.

## Conventions

### File naming

- Use kebab-case for files and folders (e.g. `manage-data-streams.md`)
- Use `index.md` for section landing pages (not `README.md`)

### Images

- Store images in `docs/images/` under the relevant section subfolder
- Use kebab-case for image filenames
- Reference images with relative paths

### Links

- Use relative markdown links between pages (e.g. `../concepts/agent/index.md`)
- Do not hardcode version numbers in internal links

### Commit messages

Prefix all commits with `docs:` (e.g. `docs: update installation guide for stream host`)

### Alerts and admonitions

Use MkDocs Material admonition syntax:

```markdown
!!! note
    Useful information the reader should be aware of.

!!! tip
    Helpful advice for a better experience.

!!! warning
    Something the reader should be cautious about.

!!! danger
    A serious risk the reader must understand.
```

## Validation

Pull requests are automatically checked for:

- **Markdown linting** via markdownlint
- **Broken links** via lychee

Fix any reported issues before requesting review.

## Access

- **XMPro Staff (Maintainers)**: Full edit access, can merge PRs and assign issues
- **Customers/Partners (Collaborators)**: Read access, can create issues and suggest edits via forks
