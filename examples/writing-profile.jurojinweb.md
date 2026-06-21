# Writing profile — JurojinWeb (example)

Copy this into the **JurojinWeb** repo as `.claude/writing-profile.md` and verify
against the real component library. The `jurojin-writing` skill reads this to know
*how to render* what it writes here.

## Output format

- Target: **React / JSX** (FAQ & solution pages are JS modules returning JSX, e.g.
  `components/helpers/faq/*.js`).
- Content is composed from JSX/HTML tags + imported components, not markdown.

## Resources & components (cheat sheet)

### Standard elements (JSX/HTML)

| Element | Tag |
|---------|-----|
| Headings | `<h2>`, `<h3>` (classes `h4`/`h5`/`h6` for sizing) |
| Bold | `<strong>` |
| Link | `<a href="" target="_blank">` |
| Image | `<img src="" alt="" />` |
| Lists | `<ul><li>` / `<ol><li>` |
| Blockquote | `<blockquote>` |
| Divider | `<hr />` |
| Table | `<table><tbody><tr><th>/<td>` |

### Custom components (import + use)

| Component | Import | Use |
|-----------|--------|-----|
| Highlight | `import { Highlight } from "@/components/blog/RichText"` | `<Highlight>text</Highlight>` |
| CTA banner | `import { HighlightCTA } from "@/components/shared/HighlightCTA"` | `<HighlightCTA buttonText="Download Now" title="…" href="https://jurojinpoker.com/download" />` |
| Preview card | `import { PagePreviewWidget } from "@/components/shared/PagePreviewWidget"` | `<PagePreviewWidget href="https://jurojinpoker.com/en/solution/SLUG" />` |
| Video embed | — | `<iframe src="…" allow="…" />` (Cloudinary/Gyazo/YouTube) |

<!-- TODO: confirm the full component set and props, and the web equivalents for
     Strapi's [features](slug) table, [x] embed, and [[card]] visuals if any. -->

### Mapping vs the Strapi blog (same logical element, different syntax)

| Logical element | Strapi (markdown) | JurojinWeb (React) |
|-----------------|-------------------|--------------------|
| Highlight | `==text==` | `<Highlight>text</Highlight>` |
| CTA banner | `[bigText \| ctaText](url)` | `<HighlightCTA buttonText title href />` |
| Preview card | `[preview](url)` | `<PagePreviewWidget href={url} />` |

## Conventions

- Imports at the top of the file, grouped.
- Deep links to the client use the `jurojin:store*` scheme — use the canonical
  CTA wording established for the piece, not ad-hoc copy.
- Prefer components over raw markup so styling stays consistent.
<!-- TODO: note any page frontmatter/metadata the route needs (title, slug, seo). -->

## Example (FAQ entry rendered here)

```jsx
import { PagePreviewWidget } from "@/components/shared/PagePreviewWidget";

<>
  <h2 className="h4">Do my room plugins update automatically?</h2>
  <p>Yes — your plugins update when you launch Jurojin. If one is missing, see{" "}
    <a href="/help/reinstalling-plugins">Reinstalling plugins</a>.</p>
  <PagePreviewWidget href="https://jurojinpoker.com/en/solution/overlays-quick-tour" />
</>
```
