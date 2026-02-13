This is my personal academic website built with [Hugo](https://gohugo.io/) and the [Hello Friend NG](https://github.com/rhazdon/hugo-theme-hello-friend-ng) theme.

## Quick Start

### Local Development

```bash
# Start development server
hugo server
```

The site will be available at `http://localhost:1313`

### Build for Production

```bash
# Build the static site
hugo
```

Output will be in the `public/` directory.

## Project Structure

- `content/` — Blog posts, publications, code projects, and talks
- `config.toml` — Site configuration
- `themes/hello-friend-ng/` — Active theme
- `static/` — Static assets (images, etc.)
- `public/` — Generated site (not committed)

## Content Sections

- **Home** — About & biography
- **Blog** — Posts on economics and data science
- **Publications** — Peer-reviewed research papers
- **Code** — Open-source software and R packages
- **Talks** — Conference presentations and seminars

## Deployment

Deployed on [Netlify](https://www.netlify.com/) with automatic builds from the `master` branch.

## License

Licensed under the [MIT License](LICENSE.md).
