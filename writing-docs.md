---
title: Writing Docs for this Repo
description: How to write documents in this repository and how libdoc and 11ty convert them to the site deployed at forengers-docs.vercel.app
layout: libdoc_page.liquid
permalink: writing-docs.html
tags:
  - docs
  - libdoc
  - 11ty
tocEnabled: true
date: false
eleventyNavigation:
  key: Writing Docs for this Repo
  order: -1
---

## Overview

This repository uses Eleventy with the libdoc framework to transform Markdown files into a static site served at `forengers-docs.vercel.app`.

We create plain Markdown files with a YAML front matter block at the top. Eleventy + libdoc read that metadata and render the page using the `libdoc_page.liquid` layout and the site's templates and data.

## File front matter (required fields)

Every published document in this repo should start with YAML front matter. The minimal useful fields are:

- `title`: The human-facing page title.
- `layout`: Typically `libdoc_page.liquid` in this project so the page is wrapped in the standard site chrome.
- `permalink`: The output HTML filename or path (for example `shadcn.html` or `guides/my-page/index.html`).
- `tags`: Array of tags used by the site (optional but helpful for navigation).
- `tocEnabled`: `true` or `false` to enable/disable the automated table of contents for the page.
- `date`: Date or `false` (if you don't want an automatic date).

Example front matter (from `writing-docs.md`):

```yaml
---
title: Writing Docs for this Repo
description: How to write documents in this repository and how libdoc and 11ty convert them to the site deployed at forengers-docs.vercel.app
layout: libdoc_page.liquid
permalink: writing-docs.html
tags:
  - docs
  - libdoc
  - 11ty
tocEnabled: true
date: false
eleventyNavigation:
  key: Writing Docs for this Repo
  order: -1
---
```

Notes:
- `permalink` controls the final URL. If you omit it, Eleventy will generate one from the file path.
- `eleventyNavigation` helps libdoc/Eleventy put the page into site navigation.

## Where to put files

- Top-level Markdown files (like `writing-docs.md`) are acceptable and will be processed.
- You can create subfolders to organize content (for example `guides/`, `reference/`, `posts/`). If you want a URL like `/guides/foo.html`, either place `foo.md` in `guides/` or set `permalink` explicitly.
- Assets (images, downloads) should go in an `assets/` folder and be referenced with relative paths from the Markdown file. Built output lands in `_site/`.

## Writing content — conventions and examples

- Use Markdown for text. Keep structure readable: short paragraphs, headings, and code blocks.
- Use the existing files as style guides.
- If you need UI component examples, include code fences with the language (for example `tsx` for React/TypeScript snippets).

Example snippet (from `shadcn.md`) showing how a component usage is documented:

```tsx
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select";

<Select onValueChange={field.onChange} value={field.value}>
  <FormControl>
    <SelectTrigger>
      <SelectValue placeholder="Choose a subject of enquiry" />
    </SelectTrigger>
  </FormControl>
  <SelectContent>
    <SelectItem value="Partner With Us">Partner With Us</SelectItem>
    <SelectItem value="Join Us">Join Us</SelectItem>
  </SelectContent>
</Select>
```

## How libdoc / Eleventy converts files to pages

- Eleventy reads each Markdown file and its front matter, then renders the content through Liquid templates provided in `_includes/` and layout files (e.g., `libdoc_page.liquid`).
- The libdoc library adds helpers and partials for documentation sites: navigation, table-of-contents, fuzzy search index generation, and consistent page chrome.
- Site configuration and data live in `_data/` (for example `libdocConfig.js`, `libdocFunctions.js`). These files customize site-wide behavior such as the search index, feed generation, and nav structure.

Key libdoc features used here:
- automatic navigation generation
- per-page table of contents via `tocEnabled`
- search index and fuzzy search (`fuzzy.js` / `fuzzy_index.json` generated during build)

## Build & deploy (local)

- Local development (live reload): run the Eleventy dev server.

  - Command (from project root): `pnpm dev`
  - This runs the script `pnpm exec eleventy --serve` as defined in `package.json` and serves the site locally with live reload.

- Build for production (static output):

  - Command: `pnpm build`
  - This runs `pnpm exec eleventy` and writes output to the `_site/` directory by default.

Quick checklist before pushing a change:
- Run `pnpm dev` to preview locally and verify the page renders correctly.
- Run `pnpm build` and inspect `_site/` to confirm the generated HTML and assets.
- Commit and push. Vercel will pick up the change and build/deploy automatically.

## Useful references

- **Libdoc docs:** [https://eleventy-libdoc.netlify.app/](https://eleventy-libdoc.netlify.app/)
- **Eleventy:** [https://www.11ty.dev/](https://www.11ty.dev/)