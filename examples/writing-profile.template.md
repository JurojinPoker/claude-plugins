# Writing profile — <REPO NAME>

Save this file in your repo at **`.claude/writing-profile.md`**. The
`jurojin-writing` skill reads it to know *how to render* content here. It owns the
**how-to-render** half of the contract; the plugin owns *what to say* and
`business.md` owns *the facts and voice*.

Fill every `<…>` / `TODO` with your repo's real values, then delete the guidance.

## Output format

- Target: `<markdown CMS | React/JSX | MDX | plain markdown | …>`
- <Rendering notes: file types, where content goes, draft/publish rules, etc.>

## Resources & components (cheat sheet)

The writer uses this to enrich pieces with real elements, not just prose.

### Standard elements

| Element | Syntax in this repo |
|---------|---------------------|
| Heading | `<…>` |
| Bold | `<…>` |
| Link | `<…>` |
| Image | `<…>` |
| List | `<…>` |
| Blockquote | `<…>` |
| Divider | `<…>` |

### Custom elements / components

List the repo-specific widgets that add value (preview cards, CTA banners, video
embeds, feature tables, highlights, …). Include import (if any) and when to use.

| Component | Import / syntax | When to use |
|-----------|-----------------|-------------|
| `<name>` | `<…>` | `<…>` |
<!-- TODO: add every custom element a writer should reach for. -->

## Conventions

- <Imports / where they go, if applicable.>
- <Frontmatter or metadata the page/record needs (title, slug, seo, …).>
- <Link schemes (e.g. `jurojin:store*` deep links), limits (bullets per list), etc.>

## Example (a short rendered snippet)

```<lang>
<a small example showing standard + at least one custom element in this format>
```
