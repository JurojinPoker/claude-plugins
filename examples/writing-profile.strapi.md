# Writing profile — Blog / Strapi CMS (example)

Copy this into the **blog (Strapi)** repo as `.claude/writing-profile.md` and keep
it in sync with the blog renderer. The `jurojin-writing` skill reads this to know
*how to render* what it writes here.

## Output format

- Target: **Markdown for the Strapi CMS** (the `shared.rich-text` body field).
- Renders on the web through the blog's custom renderer — write markdown + the
  custom shortcodes below, not React.
- Articles are created in **draft** (`publishedAt: null`); never auto-publish.

## Resources & components (cheat sheet)

> The custom elements only work in the Jurojin blog renderer, not in plain
> markdown editors. Source of truth for these: Notion → "Markdown Reference —
> Jurojin Blog Writer Agent".

### Standard elements

| Syntax | Result |
|--------|--------|
| `**text**` | Bold |
| `` `text` `` | Inline code |
| `:emoji:` | Emoji |
| `# H1` / `## H2` / `### H3` | Headings (max 3 levels) |
| `---` | Divider |
| `> text` / `> - Author` | Blockquote (optional attribution) |
| `![Alt](https://url)` | Small image |
| `[text](https://url)` | Link |

### Custom elements ⚠️ (Jurojin renderer only)

| Syntax | Result — when to use |
|--------|----------------------|
| `==text==` | Highlight — colored background on text |
| `[bigText \| ctaText](https://url)` | Link Banner — full-width banner with CTA button (standard final CTA) |
| `[preview](https://jurojinpoker.com/en/solution/SLUG)` | PreviewPage widget — visual card with thumbnail, title, description of the target |
| `\|\|https://video-url\|\|` | Horizontal video embed |
| `\|\|short:https://video-url\|\|` | Vertical video embed (shorts/mobile) |
| `[x](https://x.com/user/status/...)` | X/Twitter post embed |
| `[features](SITE-SLUG)` | Auto-generated table of Jurojin features for that room |
| `[[JC]]` `[[KS]]` … | Playing-card visual (Rank A K Q J T 9…2 / Suit H D C S) |

Usage notes:
- `[features](SITE-SLUG)` valid slots: `ggpoker`, `pokerstars`, `888poker`,
  `partypoker`, `wpn`, `ipoker`, `winamax`, `chico`, `natural8`
  (full list: https://jurojinpoker.com/features).
- Standard final CTA for `news`: `[Haven't tried Jurojin yet?|Download Now](https://jurojinpoker.com)`.

## Conventions

- Frontmatter / Strapi fields the article needs: `title`, `slug`, `coverUrl`,
  `coverAlt`, `metaTitle`, `metaDescription`, `metaKeywords`, `wordCount`,
  `hasTableOfContent`, `lang` (ID), `blocks` (dynamic zone). See the blog repo's
  own docs for the full schema.
- H2 for main sections, H3 for subsections; `---` between main sections.
- Bullets: max 6–7 per list. Images always with descriptive alt + filename title.

## Example (news body excerpt rendered here)

```markdown
- *Key point in italic.*

---

Opening paragraph: context of the announcement, why it matters.

[features](wpt)

## Feature 1: Name

What it is and the concrete benefit for the grinder.

[preview](https://jurojinpoker.com/en/solution/betsizes-overlay)

---

# Get Started

[Haven't tried Jurojin yet?|Download Now](https://jurojinpoker.com)
```
