# Writing profile — Blog / Strapi CMS (example)

Copy this into the **blog (Strapi)** repo as `.claude/writing-profile.md` and
adjust to the real CMS resources. The `jurojin-writing` skill reads this to know
*how to render* what it writes here.

## Output format

- Target: **Markdown for the Strapi CMS** (rich-text / markdown field).
- Renders on the web through the blog's component mapping — write the markdown +
  shortcodes the renderer understands, not React.

## Available resources / shortcodes

<!-- TODO: replace with the real shortcodes/blocks the renderer supports. -->

| Intent | Shortcode / block | Example |
|--------|-------------------|---------|
| Callout / note | `:::callout{type="info"}` ... `:::` | info / warning / tip |
| Accordion (FAQ) | `:::accordion` with `### Question` items | one `###` per question |
| Image | `![alt](/uploads/...)` or media block | use uploaded media ids |
| CTA block | `:::cta{href="..."}` Label `:::` | canonical CTA wording |
| Code / steps | standard markdown ordered list | numbered steps |

## Conventions

- Frontmatter the CMS expects (title, slug, excerpt, cover) goes at the top.
  <!-- TODO: list the exact fields. -->
- Reference uploaded media by the CMS path/id; flag a missing asset as `TODO:`.
- Keep to markdown + supported shortcodes; raw HTML may be stripped/sanitized.
  <!-- TODO: confirm whether raw HTML is allowed. -->

## Example (FAQ entry rendered here)

```markdown
:::accordion
### Do my room plugins update automatically?
Yes — your plugins update when you launch Jurojin. If one is missing, see
[Reinstalling plugins](/help/reinstalling-plugins).
:::
```
