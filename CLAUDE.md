# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev        # Hugo dev server with live reload
npm run build      # Production build (minified, to /public)
npm run preview    # Production build with metrics output
npm run format     # Format all templates/code with Prettier
npm run update-modules  # Update Hugo modules to latest versions
```

Hugo requires extended edition (v0.121.2+) and Go (v1.20.5+).

## Architecture

This is a **Hugo static site** (theme: Hugoplate) for the LIMMS research laboratory. Content is Markdown with YAML frontmatter; layouts are Go HTML templates; styling uses Tailwind CSS v3 compiled through PostCSS.

**Content** lives in `content/english/` — single-language site. Key collections:
- `members/` — team profiles (frontmatter-driven: photo, role, bio, social links)
- `blog/` — posts
- Root `.md` files — flat pages for Publications, Conferences, Patents, Collaborations, EURA-LIMMS, SMMIL-E, KIKO, Contacts

**Layouts** in `layouts/` override theme templates. The theme base is in `themes/hugoplate/layouts/`. Hugo's lookup order means `layouts/` always wins over `themes/`.

**Styling**: Tailwind config is in `tailwind.config.js`; custom SCSS lives in `assets/scss/custom.scss`. PurgeCSS runs on production builds. Font and color tokens come from `data/theme.json`.

**Modules**: Hugo modules (sourced from `github.com/gethugothemes/`) provide UI components (accordion, tabs, modal, gallery), shortcodes (button, notice), icons (Font Awesome), SEO helpers, and PWA support. Module imports are listed in `config/_default/module.toml`.

**Config**: `config/_default/` holds `hugo.toml` (core settings), `params.toml` (theme feature flags), `menus.en.toml` (nav structure), `languages.toml`, and `module.toml`.

**Navigation** is defined entirely in `config/_default/menus.en.toml`. Adding a new top-level page requires both a content file and a menu entry.

**Build output** goes to `public/` (gitignored). Deployment targets: Netlify (`netlify.toml`), Vercel (`vercel.json` + `vercel-build.sh`), AWS Amplify (`amplify.yml`).
