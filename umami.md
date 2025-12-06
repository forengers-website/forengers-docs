---
title: Using Umami Analytics in Our Project
description: Why we use Umami, how it works, and how analytics events are integrated into our codebase.
layout: libdoc_page.liquid
permalink: umami.html
tags:
    - analytics
    - umami
    - tracking
    - website-metrics
tocEnabled: false
date: false
eleventyNavigation:
    key: umami
---

## Table of Contents
1. [Why We Use Umami](#why-we-use-umami)
2. [How Umami Works](#how-umami-works)
3. [What Umami Tracks](#what-umami-tracks)
4. [How We Use Umami in Code](#how-we-use-umami-in-code)
5. [List of All Tracking Events Used](#list-of-all-tracking-events-used)    

---

## Why We Use Umami

Our project uses **Umami Analytics**, a privacy-focused, open-source analytics platform that helps us understand website visitor behavior **without storing personal data or using cookies**.

### ⭐ Key Benefits

- **🔐 Privacy-first (GDPR compliant)**  
  No cookies, no fingerprinting, no personal tracking.

- **📊 Useful insights without violating privacy**  
  Only aggregated, anonymous metrics are collected.

- **⚡ Extremely lightweight**  
  The script is small and does not affect performance.

- **🎯 Event-based analytics**  
  We can track specific CTAs, popups, and form submissions.

- **🔍 Helps monitor website growth**  
  Useful for measuring which pages and CTAs perform best.

---

## How Umami Works

Umami runs a tiny JavaScript script on the website.  
Each time a user visits a page or interacts with a tracked element, Umami anonymously logs that interaction.

### Behind the scenes:

1. **User visits our website**  
   The browser automatically sends technical data:
   - IP address (anonymized)
   - Browser & OS
   - Screen size
   - Page path
   - Referring source (Instagram, Google, Linktree, etc.)

2. **Umami does not use cookies**  
   No data is saved on the user’s device.

3. **Events are recorded**  
   When a user interacts with any element containing:  
   `data-umami-event="Event Name"`  
   Umami logs it.

4. **Dashboard visualization**  
   Metrics include:
   - Page views
   - Visitors
   - Top pages
   - Browsers & devices
   - Referrers
   - Event activity
   - Traffic charts

This gives our team clear insights into user behaviour.

---

## What Umami Tracks

From our privacy policy:

> When a user visits our website, Umami collects technical information such as anonymized IP addresses, browser type, operating system, device information, referring URLs, pages visited, and timestamps.  
> **Our Website does not use cookies for tracking.**

### Umami records:
- Page views  
- Session duration  
- Device & browser type  
- Referrer sources  
- Custom event interactions (CTA clicks, form submissions, etc.)

### Why this matters
This allows us to understand:
- Which pages get the most visits  
- Which CTAs users click  
- How many users reach the Razorpay donation page  
- Traffic sources and user journeys  
- Full conversion paths (Join Us → Submit → Thank You)

---

## How We Use Umami in Code

We use custom event tracking with:

```html
data-umami-event="Event Name"
```

Whenever a user clicks an element containing this attribute, Umami logs the event under that exact name.

---

## List of All Tracking Events Used

This document provides a complete reference of all **Umami Analytics events** used in the project and where each event is triggered.


### 1. Dialog.tsx — Popup Events

```html
data-umami-event="Join Us - Popup"
data-umami-event="Monthly Plan - Popup"
```


### 2. StickyNavbar.tsx — Navigation Button Events

Inside ACTION_BUTTONS:

```html
umamiEvent: "Join Us - Navbar"
umamiEvent: "Donate - Navbar"
```

Used inside the component as:

```html
data-umami-event={button.umamiEvent}
```

This tracks when a user clicks Join Us or Donate from the navbar.


### 3. DonateAction.tsx — Razorpay Redirect Event

```html
data-umami-event="Razorpay Page"
```

Fires when a user opens the Razorpay donation page.


### 4. JoinUsForm.tsx — Form Submission Event

```html
data-umami-event="Join Us - Submit Btn"
```

Tracks how many users complete the Join Us form and press Submit.


### 5. index.astro — Homepage CTA Events

```html
data-umami-event="Join Us - HeroSection"
data-umami-event="Monthly Plan - HeroSection"
```

Tracks engagement with the primary CTA buttons in the hero section.

--- 
