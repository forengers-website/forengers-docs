---
title: Image Compression Utility on Google Colab
description: How to use the CompressImages.ipynb script to compress images to WebP / AVIF and produce a zip of outputs.
layout: libdoc_page.liquid
permalink: imagecompression.html
tags:
    - image
    - compression
    - colab
tocEnabled: true
date: false
eleventyNavigation:
    key: CompressImages - Colab Notebook
---

## Overview

This page documents [**CompressImages.ipynb**](https://colab.research.google.com/drive/1N2O9Ukg_5GYWuE-xhS8JXpk0rfDgNv7f) — a small utility that resizes and converts images from an `input/` folder into compressed WebP (and optionally AVIF) files in an `output/` folder, and finally zips the outputs.

**The goal:** quick, reproducible, and configurable compression for large image batches.

---

## Usage — step-by-step

1. Create `input` and `output` folders at the project root (or notebook working directory) on Google Colab.
2. Add JPGs to be compressed to the `input` folder.
3. Run all the cells except the last one. This will compress the files and store the results in the `output` folder and as an `images.zip` file.
4. Download the files - `images.zip` or individual images as needed.
5. Run the last cell to delete the files from the runtime so that new conversions can be made without the old files being compressed again.

## Prerequisites

The script relies on:

- Python with Pillow (PIL)
- `cwebp` CLI (for WebP conversion)
- `avifenc` CLI (optional, for AVIF conversion)

The dependency installations are taken care of by the cells within the notebook itself.

## How It Works Under the Hood

The script iterates over files in the `input` folder.

For supported images it:

1. Opens with Pillow (PIL).
2. Resizes the image if either dimension > `max_dim` preserving aspect ratio (uses `Image.LANCZOS`).
3. Saves a temporary PNG file.
4. Calls `cwebp` with configured `webp_options` to write `<basename>.webp` into `output_dir`.
5. Optionally calls `avifenc` with `avif_options` to write `<basename>.avif`.
6. Removes the temporary PNG.

After all conversions a zip of the output folder is created (e.g. `images.zip`).