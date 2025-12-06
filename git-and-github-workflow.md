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
3. [Getting started](#getting-started)
4. [Daily workflow](#daily-workflow)
5. [Deployment rules](#deployment-rules)
6. [Handling accidental deletions](#restoring-deleted-file)


---

## Purpose & Overview

Our workflow is designed for speed and simplicity. We use two primary branches:

*   **`main` (Production)**: This branch is locked and directly linked to Vercel for production deployments. **Never push directly to `main`.**
*   **`master` (Development)**: This is our central collaboration branch. All development happens here.

**The Golden Rule:** We push code directly to `master`. If the commit author matches our official email, Vercel automatically deploys the changes to production.

---

## Prerequisites

*   **Node.js**: LTS version recommended.
*   **pnpm**: Installed globally (`npm i -g pnpm`). We do not use `npm` or `yarn`.
*   **Git**: Configured on your machine.
*   **Access**: You must be a member of the Forengers GitHub organization.

---

## Getting started

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/forengers-website/forengers.in.git
    cd forengers.in
    ```

2.  **Switch to the working branch:**
    ```bash
    git checkout master
    ```

3.  **Install dependencies:**
    ```bash
    pnpm install
    ```

4.  **Start the development server:**
    ```bash
    pnpm run dev
    ```

---

## Daily workflow

Follow this routine to ensure smooth collaboration and successful deployments.

1.  **Sync with the team:**
    Always pull before starting work to avoid conflicts.
    ```bash
    git pull origin master
    ```

2.  **Make your changes:**
    Edit files, fix bugs, or add features.

3.  **Test locally:**
    Verify your changes work as expected.
    ```bash
    pnpm run dev
    ```

4.  **Stage your changes:**
    ```bash
    git add .
    ```

5.  **Configure Commit Identity (Crucial):**
    Vercel only deploys commits from our official email. Set this *locally* for the repo.
    
    ```bash
    git config --local user.email "forengers.help@gmail.com"
    ```

6.  **Commit:**
    ```bash
    git commit -m "Brief description of what you changed - YourName"
    ```

7.  **Push to `master`:**
    ```bash
    git push origin master
    ```

---

## Deployment rules

*   **Target Branch**: All code goes to `master`.
*   **Production**: The `main` branch is updated from `master` branch.

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
