---
title: Git & GitHub — How We Use Them 
description: Repository workflow, branch policy, commit rules, build/deploy steps, and developer guidelines for contributing to forengers.in
layout: libdoc_page.liquid
permalink: git-and-github-workflow.html
tags:
    - git
    - github
    - workflow
    - developer-onboarding
tocEnabled: true
date: false
eleventyNavigation:
    key: Git & GitHub (workflow)
---

## Table of contents

1. [Purpose & Overview](#purpose--overview)
2. [Prerequisites](#prerequisites)
3. [Getting started — clone, install, branches (start → finish)](#getting-started--clone-install-branches-start--finish)
4. [Daily workflow (edit → build → preview → commit → push)](#daily-workflow-edit--build--preview--commit--push)
5. [Branching policy & deployment rules](#branching-policy--deployment-rules)
6. [Commit & signing rules (why we set local user.email)](#commit--signing-rules-why-we-set-local-useremail)
7. [How to avoid committing a deletion (the .env.example case)](#how-to-avoid-committing-a-deletion-the-envexample-case)
8. [Useful Git commands and examples (copy-paste)](#useful-git-commands-and-examples-copy-paste)
9. [PR, review and merge expectations](#pr-review-and-merge-expectations)
10. [Troubleshooting common problems](#troubleshooting-common-problems)
11. [Appendix: evidence & references](#appendix-evidence--references)

---

## Purpose & Overview

This document explains how we use Git and GitHub for `forengers.in`. It covers our workflow, build process, and deployment rules.

We use `main` for production (managed by Vercel). Day-to-day work happens directly on `master` or on feature branches for risky changes.

---

## Prerequisites

* Node.js installed (LTS recommended).
* pnpm installed globally (`npm i -g pnpm`). We use `pnpm`, not `npm` or `yarn`.
* Git installed and configured.
* Access to the project GitHub organization and the repository you’ll be working on.
* (Optional) VS Code or your preferred editor.

---

## Getting started — clone, install, branches (start → finish)

1. Clone the github repo on your machine:

```bash
git clone https://github.com/forengers-website/forengers.in.git
cd forengers.in
```

2. Switch to the `master` branch from the default `main`:

```bash
git checkout master
```

> **Why master?** We work on `master` because `main` is directly linked to production on Vercel. We commit all changes to `master` and control deployment through Vercel. **General rule: Do not touch `main`.**

3. Run `pnpm install` to install all the deps:

```bash
pnpm install
```

4. Do the changes you want, then run `pnpm run build` to build the static website:

```bash
pnpm run build
```

5. Run `pnpm run preview` to view the built website on localhost:

```bash
pnpm run preview
```

6. Use `git config` to sign future commits with our official ID (required for Vercel deployment):

```bash
git config --local user.email "forengers.help@gmail.com"
```

7. Stage and commit your changes:

```bash
git add .
git commit -m "Commit Message with your name included"
```

8. Push to master:

```bash
git push origin master
```

---

## Daily workflow (edit → build → preview → commit → push)

We cannot rely on `pnpm run dev` due to library quirks. Follow this flow:

1. Make your changes (on `master` or your feature branch).

2. Build the project:

```bash
pnpm run build
```

3. Preview the built output locally:

```bash
pnpm run preview
# default: http://localhost:3000 (check console output)
```

Verify the built site visually in the browser and test the flows you changed.

4. Stage only the files you want to commit (avoid `git add .` unless you reviewed everything):

```bash
git add path/to/changed-file1 path/to/changed-file2
```

5. **Set the local commit email** (required for Vercel deployment to accept the commit):

```bash
git config --local user.email "forengers.help@gmail.com"
git config --local user.name "Forengers Help"
```

Run this in the repository before committing. This makes your commits appear as the official account for deployment.

6. Commit with a clear message including your name:

```bash
git commit -m "Short summary – YourName"
```

7. Push your work:

```bash
# If on master
git push origin master

# If on a feature branch
git push origin feat/<your-branch>
```

8. If you used a feature branch, open a PR to `master`.

---

## Branching policy & deployment rules

* `main`: Production, linked to Vercel. **Do not push to `main`.**
* `master`: Working branch. We usually commit directly here.
* Feature branches: Use for non-trivial or risky changes. Merge into `master` via PR.
* **Deployment**: Only commits authored by `forengers.help@gmail.com` trigger Vercel.

---

## Commit & signing rules (why we set local user.email)

Vercel’s Hobby (free) plan in our setup only accepts deployments when the commit author matches the official Forengers account/email. To ensure your work deploys:

Set local git config in the repository before committing:

```bash
git config --local user.email "forengers.help@gmail.com"
git config --local user.name "Forengers Help"
```

This only changes the git identity for the current local repository and does not affect your global settings.

If you forget and commit with another email, a quick fix is to amend the commit author before pushing:

```bash
git commit --amend --reset-author --no-edit
```

Then push.

---

## How to avoid committing a deletion (the `.env.example` case)

If you accidentally deleted `.env.example` (e.g., via `git rm`), restore it before committing:

1. **If staged but not committed:**

```bash
git restore --staged .env.example
git restore .env.example
```

2. **If already committed and pushed:**

```bash
git checkout origin/master -- .env.example
git add .env.example
git commit -m "Restore .env.example"
git push origin master
```

---

## Useful Git commands and examples (copy-paste)

Switch to master and pull:

```bash
git checkout master
git pull origin master
```

Create feature branch:

```bash
git checkout -b feat/hero-lcp-preload-yash
```

Set local commit identity for deployment:

```bash
git config --local user.email "forengers.help@gmail.com"
git config --local user.name "Forengers Help"
```

Stage only specific files:

```bash
git add src/components/common/Footer.astro src/layout/index.astro
```

Unstage a file (example to prevent deletion being committed):

```bash
git restore --staged .env.example
# if the file was removed from working tree as well, restore it:
git restore .env.example
```

Amend last commit to reset author:

```bash
git commit --amend --reset-author --no-edit
```

Push master (only after commit; ensure user.email is set locally):

```bash
git push origin master
```

Push a feature branch:

```bash
git push origin feat/hero-lcp-preload-yash
```

Revert a commit that removed a file (if already committed and pushed):

```bash
# revert the commit by its hash (example <commit-hash>)
git revert <commit-hash>
git push origin master
```

---

## PR, review and merge expectations

* Create a PR for non-trivial changes or whenever you want a review. Title the PR clearly and include the context and testing steps.
* In the PR description include: what you changed, why, local test steps (build → preview), and any risks/regressions.
* Reviewers should check accessibility changes, build output, and a visual test via `pnpm run preview`.
* Merge strategy: if approved, merge into `master`. Ensure local commit identity is set so the merge commit (if created) will be accepted by Vercel as a deployment trigger.

---

## Troubleshooting common problems

**“pnpm run dev doesn’t work”**

* Some libraries require a build step; use:

  ```bash
  pnpm install
  pnpm run build
  pnpm run preview
  ```

  Inspect the console for build errors and missing environment variables.

**Vercel not deploying my commit**

* Check the commit author/email. Use `git log -1 --pretty="%an <%ae>"` to inspect the author. If wrong, amend commit author locally and push.

**Accidentally staged a deletion**

* Use `git restore --staged <file>` then `git restore <file>` to restore from HEAD.

**You want to exclude a file from a commit**

* Stage only desired files with `git add fileA fileB` rather than `git add .`.

---

## Appendix: evidence & references

* This documentation was created using the same LibDoc structure and examples already in the docs repo.
* Reference: `Website Brainstorming and Resources.xlsx`