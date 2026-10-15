# Khoa Portfolio — public content repository

The **canonical editorial source** for khoanvm.io.vn. All four content
collections and their images are managed here through
[Pages CMS](https://app.pagescms.org).

The Astro site source, build, QA and deployment live in a separate **private**
repository, which stays private on purpose.

```text
you  ──►  Pages CMS  ──►  THIS repository (public, editorial)
                              │
                              │  automatic sync, one-way, via a reviewed PR
                              ▼
                        private Astro repository  ──►  khoanvm.io.vn
```

**Edit content here, in Pages CMS. Do not edit synchronized articles directly in
the private repository** — your change would be overwritten by the next sync.

> **Everything here is public.** Any file in this repository is world-readable on
> GitHub, including an entry marked `published: false`. That flag only controls
> whether an article appears on the website; it does not hide the file. Keep only
> publishable content here.

---

## Collections

| Collection  | Folder                       | Notes                                     |
| ----------- | ---------------------------- | ----------------------------------------- |
| Case Studies| `src/content/case-studies/`  |                                           |
| Stories     | `src/content/stories/`       |                                           |
| Insights    | `src/content/insights/`      |                                           |
| Experiences | `src/content/experiences/`   |                                           |

## Media

| Folder             | Served at          | Contents                          |
| ------------------ | ------------------ | --------------------------------- |
| `public/assets/`   | `/assets/...`      | Published images                  |
| `public/uploads/`  | `/uploads/...`     | Anything you upload through the CMS |

Image paths keep their original public URLs, so existing links never break. Do
not rename an image that is already referenced — add the new file and switch the
reference instead, because the filename is part of a permanent public URL.

## Working with images

Each image field carries its own guidance beside it in the CMS.

| Slot          | Recommended          | Format      | Target size  |
| ------------- | -------------------- | ----------- | ------------ |
| Cover         | 1600 × 800 (2:1)     | WebP        | under 250 KB |
| Story cover   | 864 × 432 (2:1)      | WebP        | under 150 KB |
| Insight cover | 800 × 400 (2:1)      | WebP        | under 250 KB |
| Listing image | ratio 37:27 (≈1.37)  | WebP        | under 120 KB |
| Gallery image | 1200–1600 px, ~3:2   | WebP        | under 200 KB |
| SEO / social  | 1200 × 630 (≈1.91:1) | WebP / JPEG | under 200 KB |
| Body image    | at most 1200 px wide | WebP        | under 200 KB |

Thumbnails render inline, because this repository is public.

### Replacing an image

Each image field holds one image, so while one is selected Pages CMS hides
Upload and Select. To replace one:

1. Press the **bin icon** on the thumbnail. This clears the reference in the
   editor only.
2. **Upload** or **Select** the replacement — both buttons reappear on the empty
   slot.
3. Check the **View on GitHub** button to open it at full size and confirm it is
   the right picture.
4. **Save**.

Clearing a reference **does not delete the file from GitHub.** The original
stays in the repository and can be re-selected at any time.

### Adding a gallery image

Press **Add** below the gallery list. That appends a new item and leaves existing
items untouched. The bin icon inside a gallery item replaces that item's image;
**Add** creates an additional one.

Body images have no single-image slot, so they can be added, changed and removed
freely.

## Alt text

Alt text is required wherever an image is set. Describe what the picture shows in
context, for someone who cannot see it. Do not start with "Image of".

---

## How a change reaches the website

1. You edit and save in Pages CMS. A commit lands in **this** repository.
2. An automatic sync opens a pull request in the private repository.
3. CI runs on that pull request.
4. A human reviews and merges.
5. Deployment is a separate, deliberate step.

**Saving does not publish the website.** Sync and deployment are distinct, and
deployment stays under manual control.
