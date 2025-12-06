---
title: How We Use shadcn/ui
description: How shadcn/ui is used on forengers.in
layout: libdoc_page.liquid
permalink: shadcn.html
tags:
    - shadcn
    - ui
    - components
tocEnabled: true
date: false
eleventyNavigation:
    key: shadcn/ui
---

## What is shadcn/ui?

**shadcn/ui** is a collection of beautifully designed, accessible React components.

**Key Characteristics**

- **Easy-to-import components**: Unlike npm packages, shadcn/ui components are designed to be copied directly into your project.
- **Highly customizable**: You can easily customize your components.
- **Accessible by default**: For good SEO.

## Top Component Libraries & Other Resources

- [Official Documentation - ui.shadcn.com](https://ui.shadcn.com)
- [Aceternity UI](https://ui.aceternity.com/)
- [React Bits](https://reactbits.dev/)
- [Mvpblocks](https://blocks.mvp-subha.me/)
- [Kibo UI](https://www.kibo-ui.com/)
- [skiper/ui](https://skiper-ui.com/)
- [tweakcn](https://tweakcn.com/)
- [Neobrutalism components](https://www.neobrutalism.dev/)

## UI Components in Our Project
Located in `src/components/ui`

**Component Structure Example: Card**

The `Card` component is a composable container system:

```tsx
// src/components/ui/card.tsx
export { 
  Card,           // Main container
  CardHeader,     // Header section
  CardTitle,      // Title within header
  CardDescription, // Subtitle/description
  CardContent,    // Main content area
  CardFooter      // Footer section
}
```

**Usage Pattern:**
```tsx
<Card>
  <CardHeader>
    <CardTitle>Title</CardTitle>
    <CardDescription>Subtitle</CardDescription>
  </CardHeader>
  <CardContent>Main content here</CardContent>
  <CardFooter>Footer actions</CardFooter>
</Card>
```

## Usage Example in the forengers.in Repo

**Select Component**

**Location:** `src/components/contact-us/ContactForm.tsx`

The Select component provides accessible dropdown functionality:

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
    <SelectItem value="Research">Research</SelectItem>
    <SelectItem value="Donations">Donations</SelectItem>
    <SelectItem value="Other">Other</SelectItem>
  </SelectContent>
</Select>
```

## Adding New Components using shadcn CLI

Install a new component from the shadcn registry:

```bash
pnpm dlx shadcn@latest add [component-name]
```

**Example:**
```bash
pnpm dlx shadcn@latest add tabs
pnpm dlx shadcn@latest add alert
```

This will:
1. Create the component file in `src/components/ui/`
2. Install required dependencies automatically
3. Update your project configuration
---
**Customizing Components**

You can customize components by modifying their files in `src/components/ui/`.