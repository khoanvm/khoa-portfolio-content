# Khoa Portfolio — public content repository (Proof of Concept)

This repository holds **published portfolio content and images** so that Pages
CMS can edit them, while the Astro site source stays private.

> **Proof of Concept.** It contains exactly one case study. It is not the
> production repository, it does not deploy, and the private repository
> `khoanvm/khoa-portfolio` remains the single source of truth for the build.

---

## What is in here

| Path                                            | Purpose                          |
| ----------------------------------------------- | -------------------------------- |
| `src/content/case-studies/audibene.md`          | One published case study         |
| `public/assets/figma/case-studies/*.png`        | Its cover and three gallery images |
| `public/uploads/`                               | Where new CMS uploads land       |
| `.pages.yml`                                    | Pages CMS configuration          |

## Safety basis

Every file here was **already world-readable** on the live site before this
repository was created:

```text
https://khoanvm.io.vn/case-studies/audibene/                         200
https://khoanvm.io.vn/assets/figma/case-studies/audibene-article.png  200
https://khoanvm.io.vn/assets/figma/case-studies/index-audibene-1.png  200
https://khoanvm.io.vn/assets/figma/case-studies/index-audibene-2.png  200
https://khoanvm.io.vn/assets/figma/case-studies/index-audibene-3.png  200
```

Nothing is disclosed here that is not already public.

## Connecting Pages CMS

1. Go to <https://app.pagescms.org> and sign in with GitHub.
2. Add repository **`khoanvm/khoa-portfolio-content`**.
3. Select branch **`main`**.
4. Grant the Pages CMS GitHub App write access.

No tokens are needed, and none should ever be pasted into this repository.

## Editing images

The inline thumbnail works here **because this repository is public**. Pages CMS
points the browser at GitHub's unauthenticated download URL, which returns 404
for a private repository — that is why thumbnails never appeared in the private
repo. See `docs/COMPATIBILITY.md` in the private repository for the full
explanation.

**Replacing an image.** Each image field holds one image, so while one is
selected Pages CMS hides Upload and Select. To replace one:

1. Press the **bin icon** on the thumbnail. This clears the reference in the
   editor only.
2. **Upload** or **Select** the replacement — both buttons reappear on the empty
   slot.
3. Check the **View on GitHub** button to confirm it is the right picture.
4. **Save**.

Clearing a reference **does not delete the file from GitHub.** The original
stays in the repository and can be re-selected at any time.

**Adding a gallery image without replacing one.** Press **Add** below the
gallery list. That appends a new item and leaves existing items untouched. The
bin icon inside a gallery item replaces that item's image; **Add** creates an
additional one.

## Image guidelines

Each image field carries its own dimensions, aspect ratio, format and target
file size in the helper text beside it. Summary:

| Slot           | Recommended           | Format | Target size |
| -------------- | --------------------- | ------ | ----------- |
| Cover          | 1600 × 800 (2:1)      | WebP   | under 250 KB |
| Gallery image  | 1200–1600 px, ~3:2    | WebP   | under 200 KB |
| SEO / social   | 1200 × 630 (~1.91:1)  | WebP or JPEG | under 200 KB |
| Body image     | at most 1200 px wide  | WebP   | under 200 KB |

## Conventions

- Image paths keep the original public convention, e.g.
  `/assets/figma/case-studies/audibene-article.png`. Existing paths are **not**
  rewritten.
- New uploads are stored as `/uploads/<filename>` and committed under
  `public/uploads/`.
- Alt text is required wherever an image is set.
- Slugs are lowercase kebab-case.
- Drafts stay out of the build (`published: false`).
