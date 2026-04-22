# XMPro Platform Documentation

Product documentation for the XMPro Platform.

**Live site**: [docs.xmpro.com](https://docs.xmpro.com)

## Versions

| Branch | Platform version | Status |
|--------|-----------------|--------|
| `main` | v4.6 | Current release |
| `v4.5` | v4.5 | Supported |
| `v4.4` | v4.4 | Legacy |
| `v5.0` | v5.0 | Pre-release |

## Quick start

```bash
# Clone and preview locally
git clone https://github.com/XMPro-Auto/xm-platform-docs.git
cd xm-platform-docs
pip install mkdocs-material mike
mkdocs serve
```

Then open [http://localhost:8000](http://localhost:8000).

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for branch targeting, conventions, and workflow details.

## Tech stack

- [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) for rendering
- [mike](https://github.com/jimporter/mike) for multi-version deployment
- GitHub Pages for hosting
- GitHub Actions for CI/CD (build, lint, link check)
